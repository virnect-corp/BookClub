# EXERCISE 2.5

Selecting the right kinds of beacons to use in code can take some practice. Use this exercise to deliberately practice using beacons in code.

## Step 1: Select code

For this exercise select an unfamiliar codebase, but do select one in a programming language that you are familiar with. If possible, it would be great to do this exercise on a codebase where you know someone familiar with the details. You can then use that person as a judge of your understanding. In the codebase, select one method or function.

**Answer**

아무래도 unfamiliar codebase 이면서 someone familiar with the details 인 코드를 찾는게 쉽지 않다는 생각임. 다른 사람들도 알만한 코드를 고려하던 중 socket client 예제 코드를 선정.

https://docs.microsoft.com/en-us/dotnet/framework/network-programming/asynchronous-client-socket-example

여기서 선택한 메서드는 StartClient()

## Step 2: Study code

Study the selected code and try to summarize the meaning of the code.

**Answer**

Host address를 준비하고 SocketClient를 준비.
이후 connect를 실행하고 간단한 text를 send, receive를 한 후에 receive한 메시지를 출력하고 client 종료.

## Step 3: Actively notice beacons that you use

Whenever you have an “aha” moment where you get a bit closer to the functionality of the code, stop and write down what it was that led you to that conclusion. This could be a comment, a variable name, a method name, or an intermediate value—all of those can be beacons.

**Answer**

``` c#
connectDone.WaitOne(); 
```

이 부분에서 왜 connectDone이라는 변수가 WaitOne()이라는 기다리는 메서드를 호출하는지 몰랐다가 ConnectCallBack method에서 connectDone.Set() 메서드 호출을 기다리고 있다는 사실을 알게 됨.
주석문 역시 `// Signal that the connection has been made.` 라고 적혀 있음.

마찬가지로 Send, Receive도 같은 관계로 Set()을 기다리고 있는 부분을 알게 됨

``` c#
// Send test data to the remote device.  
Send(client,"This is a test<EOF>");  
sendDone.WaitOne();
```

``` c#
// Signal that all bytes have been sent.  
sendDone.Set();
```

모든 바이트 값을 보낼때 까지 기다리는 의미로 사용

Receive(client);와 receiveDone.WaitOne()의 관계도 동일함.

``` c#
// Receive the response from the remote device.  
Receive(client);  
receiveDone.WaitOne();  
```

``` c#
// Signal that all bytes have been received.  
receiveDone.Set();
```

위와 같이 모든 바이트에 대해서 완료될 때 까지의 신호를 기다리는 의미로 사용함

## Step 4: Reflect

When you have a thorough understanding of the code and a list of beacons, reflect using these questions:

- What beacons have you collected?
- Are these code elements or natural language information?
- What knowledge do they represent?
- Do they represent knowledge about the domain of the code?
- Do they represent knowledge about the functionality of the code?

**Answer**

What beacons have you collected?

- connectDone, sendDone, receiveDone 등의 기다리는 변수의 표시

Are these code elements or natural language information?

- 둘 다. ManualResetEvent라는 코드의 변수 이름으로 표시되어 있음, 코멘트로 설명이 되어 있음

What knowledge do they represent?

- 비동기 소켓 프로그래밍에서 connect, send, receive에 대해서 언제 처리가 끝나고 언제까지 대기해야 하는지에 대해 알려줌

Do they represent knowledge about the domain of the code?

- 예. 기본적으로 연결이후 송신, 수신에 대해 네트워크 도메인에 대한 지식이 필요함

Do they represent knowledge about the functionality of the code?

- 예, 비동기 기능을 구현하는 방법에 대한 지식을 나타냄

## Step 5: Contribute back to the code (optional)

Sometimes, but not always, the beacons you have selected could be improved or extended. Or the code might be in need of additional beacons that aren’t there yet. This is a great moment to enrich the code with the new or improved beacons. Because you weren’t familiar with the code before this exercise, you have a good perspective on what would help someone else who is new to the codebase too.

**Answer**

비동기 callback method에 대해 미리 확인해 보고 어떤 기능을 수행하는지 먼저 살펴보면 좋을 것 같다는 생각이 듬. 만약 비동기 callback이라는 개념이 없으면 코드를 이해하기가 어려울 것이므로 관련된 코멘트를 더 추가해 볼 수 있음.

## Step 6: Compare with someone else (optional)

If you have a coworker or friend who wants to improve their beacon use too, you can do this exercise together. It can be interesting to reflect on the differences both of you had in reproducing code. Because we know there are large differences between beginners and experts, this exercise might also help you understand your level of skill in a programming language relative to someone else’s.

**Answer**

pull reqeust review 코멘트로 확인해 볼 수 있을 듯.