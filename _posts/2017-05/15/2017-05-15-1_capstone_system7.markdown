---

layout: post
title: "(캡스톤) 캡스톤[5.15]"
category: PYTHON

---

### 회고
한 10일정도 블로그에 포스트를 하지 않았다. 게을렀던 것도 있었고 개인적인 사정 또한 있었다. 인턴모집기간이라 작성해야 하는 자소서도 쌓여있고 공부해야할 것도 쌓여있다ㅠ변명은 아니지만 다시 열심히해야하는데 넘나 할게 많다.

### 오늘 할일(5월 15일)
> 오늘의 목표다.
* AWS SQS(Simple Queue Service)를 사용해보자

### Queue 만들기
* FIFO를 사용해야 하는데 Asia(Seoul)은 지원을 하지 않아 US West(Oregon)으로 여행을 떠나려 한다.

1. 이름을 입력하고(fifo를 사용할 때는 .fifo를 붙여야한다)<br/>
<img src = '/post_img/201705/15/1.png'/><br/>

2. 테스트 여서 따로 설정을 하지 않고 Quick Create로 만들었다<br/>
<img src = '/post_img/201705/15/2.png'/><br/>

### 구현
* message내에 attribute로(이런느낌) userId를 받아 추천을 진행하려 한다.<br/>
<img src = '/post_img/201705/15/3.png' height='400'/><br/>
* 이 그림은 말그대로 예제이다. 실제로는 시간표 서버에서 큐에 메세지를 보내줄 예정이다.
* Busy waiting 방식으로 EC2 서버에서 이 코드는 계속해서 돌아갈 예정이다.

```python
import boto3
from real_recommend import rec


#Connect to a session
session = boto3.Session(
    region_name="us-west-2",
    aws_access_key_id="",
    aws_secret_access_key=""
)

sqs = session.client('sqs')
queue = sqs.get_queue_url(QueueName='testQueue.fifo')

def receive_message():
    # busy waiting
    while(True):
        messages = sqs.receive_message(
            QueueUrl=queue['QueueUrl'],
            MaxNumberOfMessages=10,
            VisibilityTimeout=1,
            WaitTimeSeconds=1,
            MessageAttributeNames=['All']
        )
        # Messages가 있으면 message가 있다는 것
        if 'Messages' in messages:
            print(messages)
            # dict 형태로 넘어온다
            if 'MessageAttributes' in messages['Messages'][0]:
                rec.request_recommend(int(messages['Messages'][0]['MessageAttributes']['userId']['StringValue']))
            resp = sqs.delete_message(
                QueueUrl=queue['QueueUrl'],
                ReceiptHandle=messages['Messages'][0]['ReceiptHandle']
            )

receive_message()

###########rec 파일
# id를 넘겨받아 추천을 수행합니다.
def request_recommend(id):
    compUser = scoreCollection.find({"_id": id})
    push_recommend_data(compUser)

```

* 이러면 sendMessage를 해주면 request를 바로 처리해준다.

### 고민할 것
* response를 어떤 형태로 보낼것인가
    * 강호형과 얘기
* message의 attribute에 대해 공부해보자 : [Documents 링크](http://boto3.readthedocs.io/en/latest/reference/services/sqs.html#SQS.Queue.receive_messages)
    * **Parameters**
        * AttributeNames : return 되어야 하는 Attribute를 선택 할 수 있다.
            * All - Returns all values.
            * ApproximateFirstReceiveTimestamp - 처음 도착한 메세지만
            * ApproximateReceiveCount - 큐에서 몇번정도 요청 되어졌는지
            * SenderId
            * SentTimestamp - 큐에서 보내진 시간
            * MessageDeduplicationId - Returns the value provided by the sender that calls the `` SendMessage `` action.
            * MessageGroupId - Returns the value provided by the sender that calls the `` SendMessage `` action.
            * SequenceNumber - Amazon SQS에서 제공되는 숫자
            * ApproximateNumberOfMessages
            * ApproximateNumberOfMessagesDelayed
            * ApproximateNumberOfMessagesNotVisible
            * CreatedTimestamp
            * ContentBasedDeduplication
            * DelaySeconds
            * FifoQueue
            * LastModifiedTimestamp
            * MaximumMessageSize
            * MessageRetentionPeriod
            * Policy
            * QueueArn
            * ReceiveMessageWaitTimeSeconds
            * RedrivePolicy
            * VisibilityTimeout
        * MessageAttributeNames<br/>
        <img src = '/post_img/201705/15/4.png'/><br/>
            * string으로 입력, attribute에 userId가 들어오면 사용가능, 안들어오면 그냥 디폴트 형태의 메세지
        * MaxNumberOfMessages : 메세지 리턴 갯수, 1~10. SQS는 이 값보다 더 리턴하지 않는다.
        * VisibilityTimeout
        * WaitTimeSeconds
        * ReceiveRequestAttemptId : FIFO 큐일때만 사용가능
            * ReceiveRequestAttemptId는 ReceiveMessage이후 5분 내에 사용할 수 있음
            * You can retry the ReceiveMessage action with the same ReceiveRequestAttemptId if none of the messages have been modified (deleted or had their visibility changes).

<br/><br/>
