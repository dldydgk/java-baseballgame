# java-baseballgame
## Java를 활용하여 만든 숫자 야구 게임

#### 우선 컴퓨터가 3개의 난수를 발생시키는 메소드 playGame을 생성하고
#### 변수 x, y, z를 생성한다
#### 1~9사이에 +1을 해주고 do while문을 사용해 x, y, z 세 개의 각각 다른 난수를 발생시킨다
#### 또 출력문을 사용해 컴퓨터가 발생시킨 난수를 확인하고 리턴값을 지정한다
``` java
public static int playGame() throws IOException //컴퓨터가 3개의 난수를 발생시키는 메소드
{
	int x, y, z; //컴퓨터가 선택하는 3개 숫자
	Random r= new Random(); //난수발생 Random()메소드로 객체변수 r 생성

	x= Math.abs(r.nextInt() % 9) + 1; // 1~9 사이의 난수 발생

	do{
		y= Math.abs(r.nextInt() % 9) + 1;
		}while(y==x); // 만일 난수 y가 x와 같은 수일 때 다시 한 번 난수 발생 반복

	do{
		z= Math.abs(r.nextInt() % 9) + 1;
		}while((z==x)||(z==y)); // 만일 난수 y가 x 혹은 y와 같은 수일 때 다시 한 번 난수 발생 반복

	System.out.println(x +", "+ y +", "+ z); //컴퓨터가 발생시킨 난수 확인(게임 시 비공개)

return playGame(x, y, z);
}
```
---

### 인수 3개가 주어지는 메소드 playGame을 생성하고 게임에 필요한 변수와 배열을 생성했다
``` java
public static int playGame(int x, int y, int z) throws IOException
// 인수 3개가 주어지는 메소드
{

int count; //게임을 시도하는 횟수
int strike, ball; // 숫자 매칭에 따른 결과
int[] usr = new int[3]; // 사용자가 입력하는 숫자 3개를 저장하는 배열
int[] com = { x, y, z }; // 컴퓨터가 선택한 숫자 3개를 저장하는 배열
System.out.println("숫자 야구 게임");
count= 0;
do{
count++;
```
---
#### 메소드의 객체변수 in을 생성하고 
#### in에 들어있는 데이터들을 문자형 데이터로 저장할 변수 user를 생성했다
#### 사용자가 입력하는 숫자들을 user에 저장하고 
#### Integer(user).intValue()를 사용해 user에 저장된 데이터를 정수형으로 변환시켜 각 배열에 저장한다
``` java
do{
    System.out.println("\n카운트: "+count);
    BufferedReader in= new BufferedReader(new InputStreamReader(System.in));
    // 콘솔 화면에서 사용자가 입력하는 데이터를 받아들이는 BufferedReader() 메소드의객체변수 in 생성
    String user;//객체변수 in에 들어있는 데이터내용을 문자형데이터로 저장할 변수생성

    System.out.print("1번째 숫자: ");
    user= in.readLine(); // 사용자가 입력하는 데이터를 변수 user 에 저장
    usr[0]= new Integer(user).intValue(); //변수 user에 저장된 데이터를 정수형으로 변환시켜 배열 0번칸에 저장

    System.out.print("2번째 숫자: ");
    user= in.readLine(); // 사용자가 입력하는 데이터를 변수 user 에 저장
    usr[1]= new Integer(user).intValue(); //변수 user에 저장된 데이터를 정수형으로 변환시켜 배열 1번칸에 저장

    System.out.print("3번째 숫자: ");
    user= in.readLine(); // 사용자가 입력하는 데이터를 변수 user 에 저장
    usr[2]= new Integer(user).intValue(); //변수 user에 저장된 데이터를 정수형으로 변환시켜 배열 2번칸에 저장
```
---

### 각각의 배열들을 비교하여 모든 숫자가 1~9 사이이고 같은 숫자가 없을 경우에만 반복문을 빠져나온다
``` java
    if((usr[0]==0)||(usr[1]==0)||(usr[2]==0)){
    System.out.println("0은 입력하지 마세요. 다시 입력해주세요.");
    }else if((usr[0]>9)||(usr[1]>9)||(usr[2]>9)){
    System.out.println("1부터 9까지의 숫자 중 하나를 입력해주세요. 다시 입력해주세요.");
    }else if((usr[0]==usr[1])||(usr[1]==usr[2])||(usr[0]==usr[2])){
    System.out.println("모두 다른 숫자를 입력해주세요. 다시 입력해주세요.");
    }
        }while((usr[0]==0)||(usr[1]==0)||(usr[2]==0)||
        (usr[0]>9)||(usr[1]>9)||(usr[2]>9)||
        (usr[0]==usr[1])||(usr[1]==usr[2])||(usr[0]==usr[2]));
        //모든 숫자가 1~9사이, 같은 숫자가 없는 경우에만 반복문을 빠져나옴
```
---
### usr와 com 두 배열을 비교하여 strike와 ball의 값을 카운팅한다
### 그리고 while문을 사용해 strike가 3이 되거나 count가 11이 된다면 게임을 종료시킨다
``` java
strike = ball = 0;

    if(usr[0]==com[0]) strike++;
    if(usr[1]==com[1]) strike++;
    if(usr[2]==com[2]) strike++; //usr, com 두 개의 배열이 각각 완전히 일치할 경우에만 strike 처리

    if(usr[0]==com[1]) ball++;
    if(usr[0]==com[2]) ball++;
    if(usr[1]==com[0]) ball++;
    if(usr[1]==com[2]) ball++;
    if(usr[2]==com[0]) ball++;
    if(usr[2]==com[1]) ball++; //usr, com 두 개의 배열의 데이터 위치가 다른 경우에만 ball 처리

System.out.println("Strike: "+ strike +" Ball: "+ ball);

	}while((strike<3)&&(count<11)); //strike<3(게임미완성),count<11(시도횟수 10번까지)일 때 반복실행
	//strike=3 이거나 count=11(시도횟수 11번째)가 되면 종료

return count;
}
```
---

#### result라는 정수형 변수를 생성했다. 이 변수는 게임의 결과를 저장하기 위해 사용된다.
#### args.length==3 조건을 사용하여  3개의 값이 주어진 경우를 확인하고 주어진 인수를 정수형으로 변환하여 x, y, z 변수에 저장한다
#### 난수를 발생하여 게임을 진행하는 경우에는 playGame() 메소드를 호출하여 게임을 실행한다. 
#### 게임 실행이 완료되면, 결과값은 result 변수에 저장된다
#### result의 값에 따라 조건문을 사용하여 적절한 메시지를 출력합니다. result가 2 이하인 경우 "참 잘했어요!", 3에서 5 사이인 경우 "잘했어요!", 6에서 9 사이인 경우 "보통이네요!", 그리고 10 이상인 경우 "분발하세요!"라는 메시지가 출력되도록 하였다
``` java
public static void main(String[] args) throws IOException
{
	int result; //게임 결과값을 위한 변수 생성

    if(args.length==3){ // 게임실행 주어진 3개인 경우, 각각 정수형으로 형변환을 통해 x,y,z 에 저장
    int x= Integer.valueOf(args[0]).intValue();
    int y= Integer.valueOf(args[1]).intValue();
    int z= Integer.valueOf(args[2]).intValue();

	result= playGame(x, y, z);
		}else{ // 난수발생시키는 경우 즉, playGame()에 해당
            result= playGame(); // return 값 즉, 시도횟수(count)를 결과값으로 반환하여 result에 저장
            }

        System.out.println();
        if(result<=2){
        System.out.println("참 잘했어요!"); //시도횟수가 2번 이하
        }else if(result<=5){
        System.out.println("잘했어요!");//시도횟수가 3번부터 5번 이하
        }else if(result<=9){
        System.out.println("보통이네요!"); //시도횟수가 6번~9번
        }else{
        System.out.println("분발하세요!");// 시도횟수가 10번
        }

}
```
## 결과
![image](https://github.com/dldydgk/java-baseballgame/assets/126844590/264668e1-004f-4b61-9261-34800c867508)

