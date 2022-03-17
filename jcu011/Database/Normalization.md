# 정규화 Normalization
* [위키백과](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94)
* [참고블로그1](https://rebro.kr/159)

<br> <br> <br>

### 정규화가 생겨난 배경

한 릴레이션(Relation)에 여러 엔티티의 속성을 혼합하면 정보가 중복 저장되며 저장 공간을 낭비하게 된다.

또 중복된 정보로 인해 **이상 현상**이 발생하게 된다. 이러한 문제를 해결하기 위해 정규화 과정을 거치는 것이다. 

<br> <br> <br>

### 정규화란 ?
* Attribute 간의 종속성으로 인한 이상현상이 발생하는 관계를 분해하여 재디자인함으로써 **이상현상을 없애는 과정**
* **데이터의 중복 방지**, 무결성을 충족하기 위해 데이터베이스를 설계하는 방법
* 정규화에는 3가지 원칙이 있다.
    1. 정보의 무손실 : 분해된 릴레이션이 표현하는 정보는 분해되기 전의 정보를 모두 포함해야 한다.
    2. 최소 데이터 중복 : 이상 현상을 제거, 데이터 중복을 최소화
    3. 분리의 원칙 : 하나의 독립된 관계성은 하나의 독립된 릴레이션으로 분리해서 표현



<br> <br> <br>

### 이상현상
* 테이블 내의 데이터들이 불필요하게 **중복**되어 테이블을 조작할 때 발생되는 **데이터 불일치 현상**

1. 삽입 이상 (insertion anomaly)
    * 어떠한 특정 사실은 전혀 기록되지 않는 경우가 발생
    * 아래의 그림은 course code가 없는 데이터를 삽입할 수 없어, 
        course code를 null로 하지 않는 이상 새 교수를 테이블에 추가할 수 없다.
    ![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5c/Insertion_anomaly.svg/420px-Insertion_anomaly.svg.png)

<br>

2. 삭제 이상 (deletion anomaly)
    * 데이터의 삭제가 전혀 다른 사실에 대한 데이터의 삭제도 필요로 하게 되는 현상
    * 아래의 그림에서 ENG-206 강의를 중단시 Dr. Giddens의 모든 정보가 삭제된다.
    ![](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2c/Deletion_anomaly.svg/420px-Deletion_anomaly.svg.png)

<br>

3. 갱신 이상 (update anomaly)
    * 같은 정보가 복수개의 행에서 표현되어서 갱신은 논리적인 모순을 낳게 된다.
    * 아래의 그림에서 특정 직원의 주소 변경시 여러개의 레코드를 수정하여야 한다. 
        Employee 519는 하나의 레코드의 주소만 변경되어 다른 레코드에서 다른 주소를 가지고 있다.
    ![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/12/Update_anomaly.png/420px-Update_anomaly.png)


<br> <br> <br>

## 정규화의 종류
* 제1 정규형
* 제2 정규형
* 제3 정규형
* BCNF 정규형

### 제1 정규형 (1NF)

1차 정규형은 각 로우마다 컬럼의 값이 1개씩만 있어야 한다. 이를 컬럼이 원자값(Atomic Value)를 갖는다고 한다.

예를들어, 아래의 두 테이블은 제1 정규형을 만족하지 못한다.

<br>

* **Customer Table 1** 
    | Customer ID | Name | Telephone Number |
    |:-----:|:-----:|:--------------:|
    | 123 |	Robert | 555-861-2025 |
    | 456 | Jane | 555-403-1659, 555-776-4100, 555-808-2599 |
    | 789 | Maria | 555-808-9633 |

<br>

* **Customer Table 2** 
    | Customer ID | Name | Tel. No. 1 | Tel. No. 2 | Tel. No. 3 |
    |:-----:|:-----:|:------------:|:-----------:|:-----------:|
    | 123 |	Robert | 555-861-2025 | | |
    | 456 | Jane | 555-403-1659 | 555-776-4100 | 555-808-2599 |
    | 789 | Maria | 555-808-9633 | | |

<br>

제1 정규형을 적용시키면 아래와 같은 테이블로 나타낼 수 있다.

* **Customer Table**
    | Customer ID | First Name | Telephone Number |
    |:-----:|:-----:|:-----:|:--------------:|
    | 123 |	Robert | 555-861-2025 |
    | 456 | Jane | 555-403-1659 |
    | 456 | Jane | 555-776-4100 |
    | 456 | Jane | 555-808-2599 |
    | 789 | Maria | 555-808-9633 |

하지만 위 테이블은 갱신이상을 발생시킨다.

해당 문제는 2NF에서 해결이 가능하다.

<br> <br>

### 제2 정규형 (2NF)

제1정규형에 속하는 테이블이 제2정규형을 만족하기 위해서는 

부분 함수 종속을 제거하고 모든 속성이 기본키에 완전 함수 종속되도록 분해해야 한다.

1NF 테이블에서 복합키가 없다면, 자동으로 2NF를 만족한다.

예를들어 아래의 테이블은 2NF를 만족하지 못한다.

<br>

* **종업원의 기술**
    | 종업원 | 기술 | 근무지 |
    |:-----:|:-------:|:-------:|
    | Jones	| Typing | 114 Main Street |
    | Jones	| Shorthand | 114 Main Street |
    | Jones	| Whittling | 114 Main Street |
    | Bravo	| Light Cleaning | 73 Industrial Way |
    | Ellis	| Alchemy | 73 Industrial Way |
    | Ellis	| Flying | 73 Industrial Way |
    | Harrison | Light Cleaning | 73 Industrial Way |


{종업원} 이나 {기술}은 둘다 이 테이블의 후보키는 아니다. 

{종업원}은 다수의 기술을 가지고 있으면 테이블에 한 차례 이상 나타나기 때문이고

{기술} 또한 다수의 종업원이 같은 기술을 보유하고 있을때 테이블에 한 차례 이상 나타나기 때문.

오직 복합 키 {종업원, 기술}이 이 테이블의 후보 키이다.

그런데 남은 속성인 {근무지}는 후보 키의 일부분인 {종업원}에만 영향을 받는다. 그래서 위 테이블은 2NF가 아니다.

이때, 근무지를 변경한다면 갱신이상이 발생하므로 2NF에 맞게 테이블을 2개로 나누어 재설계하면 다음과 같다.

* **종업원**
    | 종업원 | 근무지 |
    |:-----:|:-------:|
    | Jones	| 114 Main Street |
    | Bravo	| 73 Industrial Way |
    | Ellis	| 73 Industrial Way |
    | Harrison | 73 Industrial Way |

* **종업원의 기술**
    | 종업원 | 기술 |
    |:-----:|:-------:|
    | Jones	| Typing |
    | Jones	| Shorthand |
    | Jones	| Whittling |
    | Bravo	| Light Cleaning |
    | Ellis	| Alchemy |
    | Ellis	| Flying |
    | Harrison | Light Cleaning |

<br>

그러나 모든 2NF 테이블이 갱신 이상이 없는 것은 아니다.

* **대회 우승자**
    | 대회 | 연도 | 우승자 | 우승자 생년 월일 |
    |:--------:|:----:|:--------:|:--------:|
    | Des Moines Masters | 1998 | Chip Masterson | 14 March 1977 |
    | Indiana Invitational | 1998 | Al Fredrickson | 21 July 1975 |
    | Cleveland Open | 1999 | Bob Albertson | 28 September 1968 |
    | Des Moines Masters | 1999 | Al Fredrickson | 21 July 1975 |
    | Indiana Invitational | 1999 | Chip Masterson | 14 March 1977 |

우승자와 우승자 생년월일이 {대회, 연도} 키에 의해 결정되지만, 우승자와 우승자 생년월일은 여러 개의 레코드에 중복되어 나타난다. 

이 점이 갱신 이상을 불러온다. 갱신시 주의하지 않으면 우승자는 여러 개의 생일을 가질 수 있다.

이 문제는 3NF에서 해결이 가능하다.

<br> <br> 

### 제3 정규형 (3NF)
제3 정규형을 만족하려면 아래와 같은 필요충분 조건이 있다.
1. 릴레이션 R(테이블)은 제2정규형이다.
2. 릴레이션 R의 키가 아닌 모든 컬럼이 릴레이션 R의 모든 키에 이행적 종속이 되지 않는다.
    (이행적 함수종속은 기능적 종속으로 X -> Y 이고 Y -> Z 에 의해서 X -> Z (X가 Z를 결정한다)가 되는 것이다.)
    즉, 이행적 종속이 되지 않는다는 것은 테이블 내의 모든 속성이 기본 키에만 의존하며, 다른 속성에 의존하지 않는다는 것

예를들어 아래의 테이블은 3NF를 만족하지 못한다.

<br>

* **대회 우승자**
    | 대회 | 연도 | 우승자 | 우승자 생년 월일 |
    |:--------:|:----:|:--------:|:--------:|
    | Des Moines Masters | 1998 | Chip Masterson | 14 March 1977 |
    | Indiana Invitational | 1998 | Al Fredrickson | 21 July 1975 |
    | Cleveland Open | 1999 | Bob Albertson | 28 September 1968 |
    | Des Moines Masters | 1999 | Al Fredrickson | 21 July 1975 |
    | Indiana Invitational | 1999 | Chip Masterson | 14 March 1977 |

{우승자}와 {우승자 생년월일}이 {대회, 연도} 후보키에 의해 결정되지만,

우승자 생년월일은 {우승자}에 의해서 결정된다. 즉, 생년월일 속성이 기본키가 아닌 다른 속성에 의존한다.

따라서 아래와 같이 테이블을 분리하여 변형하면 3NF를 만족할 수 있다.

* **대회 우승자**
    | 대회 | 연도 | 우승자 |
    |:--------:|:----:|:--------:|
    | Des Moines Masters | 1998 | Chip Masterson |
    | Indiana Invitational | 1998 | Al Fredrickson |
    | Cleveland Open | 1999 | Bob Albertson |
    | Des Moines Masters | 1999 | Al Fredrickson |
    | Indiana Invitational | 1999 | Chip Masterson |

<br>

* **우승자 생년월일**
    | 우승자 | 우승자 생년 월일 |
    |:--------:|:--------:|
    | Chip Masterson | 14 March 1977 |
    | Al Fredrickson | 21 July 1975 |
    | Bob Albertson | 28 September 1968 |
    | Al Fredrickson | 21 July 1975 |
    | Chip Masterson | 14 March 1977 |

<br> <br>

### BCNF 정규형 (Boyce-Codd Normal Form)
BCNF 정규형은 3.5 정규형이라고도 하며 아래와 같은 필요조건이 있다.
* 3NF의 모든 요구 사항을 충족
* 후보 키가 다른 속성에 부분적으로 의존하지 않는 경우 모든 테이블은 BCNF에 있다고 한다. 
    (x, y, z) 열이있는 모든 테이블에서 (x, y)-> z 및 z-> x이면 BCNF 위반이다. 
    (x, y)가 복합 키이고 (x, y)-> z이면 직접 또는 부분적으로 역 종속성이 없어야한다.

예를들어 아래의 테이블은 3NF를 만족하지만 BCNF를 만족하지 못한다.

<br>

* **학생의 수강 신청**
    | Student | Course | Professor |
    |:----:|:-------:|:----:|
    | Chip Masterson | Machine Learning | Andrew Ng |
    | Al Fredrickson | Java Programming | James Gosling |
    | Al Fredrickson | Machine Learning | Andrew Ng |
    | Bob Albertson | Java Programming | James Gosling |
    | Chip Masterson | Algorithm | Dijkstra |

{Student, Course} 를 기본키로 선정한 경우 3NF 까지 만족하지만 삽입이상, 갱신이상, 삭제이상이 생길 수 있다.

* 삽입이상
    Algorithms 라는 수업이 Dijkstra 에 의해 열렸다고 하자. 하지만 수강생이 아무도 없는 경우 삽입할 수 없다.
* 갱신이상
    James Gosling 이 담당하는 강의가 바뀌게 될 경우 수강생의 수만큼 갱신해줘야 하므로
    하나라도 빠뜨리면 데이터 불일치 문제가 발생할 여지가 있다.
* 삭제이상
    Bob Albertson이 Java Programming수업을 수강취소하여 수강생이 없어지면 James Gosling 이라는 교수도 사라진다.

따라서 아래와 같이 테이블을 분리하면 BCNF를 만족할 수 있다.

* **학생의 수강 수업**
    | Student | Course |
    |:----:|:-------:|
    | Chip Masterson | Machine Learning |
    | Al Fredrickson | Java Programming |
    | Al Fredrickson | Machine Learning |
    | Bob Albertson | Java Programming |
    | Chip Masterson | Algorithm |

<br>

* **교수의 수업**
    | Professor | Course |
    |:-------:|:----:|
    | Andrew Ng | Machine Learning |
    | James Gosling | Java Programming |
    | Dijkstra | Algorithm |

<br> <br> <br> 
