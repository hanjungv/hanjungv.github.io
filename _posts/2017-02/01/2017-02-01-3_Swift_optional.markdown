---

layout: post
title: "(Swift) Optional이란?"
categories: SWIFT

---

-	Optional이란?
	-	스위프트에서 강력히 주장하는 Type-safe에 해당하는 속성
	-	변수 뒤에 ?를 붙여주면 *변수에 값이 있을수도 없을 수도 있다는 것을 알려준다*
	-	Optional type에서 값을 확인 쓸 때는 확인과정이 있어야 하는데
		1.	값이 있는지를 확인하고
		2.	이 값이 있으면 사용하자!
	-	이러한 과정을 unwrapping이라 한다.
	-	이런 과정을 거치게 되면 런타임 시에 nil exception으로 앱이 죽는 최악의 상황 까지는 막을 수 있다.
-	어떻게 unwrapping 해서 사용할까?

	1.	Optional binding : if let~ 으로 확인하고 값이 있으면 이 if문을 수행
	2.  Optional chaining : 만약 binding으로 체크해야 할 것이 많아지면? 몇중으로 코드가 작성될 것.
	3.	forced Unwrapping(**!**) : 값이 있든 없든 꺼내서 쓰겠다 라는 의미!<br/> 전혀 type-safe한 특성은 아닙니다. 권장하지 않는 사항!

```objective-c
	//binding예제
	var name:String? = "hanjung"
	if let Name = name{
	    let message = "hello" + Name
	    print(message)
	}

	//binding으로만
	var address: Int?
	if let home = paul.home{
	    if let postal = home.postal{
	        if let building = postal.building{
	            if let Address = building.address{
	                address = Address
	            }
	        }
	    }
	}
	//chaining. 한줄로 표현이 가능하다.
	//chaining같은 경우는 binding과 같이 쓰이는 경우도 많다.
	address = paul.home?.postal?.building?.address

	//forced unwrapping
	var number:Int!
	print(number) //error 발생!
```

<br/><br/>
