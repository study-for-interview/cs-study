# 📌 가상 메모리

## ✔ 가상 메모리 개발 배경
실행되는 코드의 전부를 물리 메모리에 존재시켜야 했고, 메모리 용량보다 큰 프로그램은 실행시킬 수 없었다. 또한, 여러 프로그램을 동시에 메모리에 올리기에는 용량의 한계와, 페이지 교체등의 성능 이슈가 발생하게 된다. 또한, 가끔만 사용되는 코드가 차지하는 메모리들을 확인할 수 있다는 점에서, 불필요하게 전체의 프로그램이 메모리에 올라와 있어야 하는게 아니라는 것을 알 수 있다.

**프로그램의 일부분만 메모리에 올릴 수 있다면...**
물리 메모리 크기에 제약받지 않게 된다.
더 많은 프로그램을 동시에 실행할 수 있게 된다. 이에 따라 응답시간은 유지되고, CPU 이용률과 처리율은 높아진다.
swap에 필요한 입출력이 줄어들기 때문에 프로그램들이 빠르게 실행된다.


## ✔ 가상 메모리가 하는 일

![](https://images.velog.io/images/kcwthing1210/post/eec91d34-9f51-4082-bd25-819dbbf8cb91/image.png)

가상 메모리는 실제의 물리 메모리 개념과 사용자의 논리 메모리 개념을 분리한 것으로 정리할 수 있다. 이로써 작은 메모리를 가지고도 얼마든지 큰 가상 주소 공간을 프로그래머에게 제공할 수 있다.

가상 메모리의 기본 아이디어는 프로세스는 가상 주소를 사용하고, 데이터를 사용(읽고/쓰기) 할 때 물리 주소로 변환해주면 된다는 것이다.

즉, 가상 메모리 시스템을 사용하기 위해서는 가상 주소(virtual address)와 물리 주소(physical address)가 필요하다.

- virtual address(가상 주소): 프로세스가 참조하는 주소
- physical address(물리 주소): 실제 메모리 주소

가상 주소 공간
한 프로세스가 메모리에 저장되는 논리적인 모습을 가상메모리에 구현한 공간이다. 프로세스가 요구하는 메모리 공간을 가상메모리에서 제공함으로써 현재 직접적으로 필요치 않은 메모리 공간은 실제 물리 메모리에 올리지 않는 것으로 물리 메모리를 절약할 수 있다.
예를 들어, 한 프로그램이 실행되며 논리 메모리로 100KB 가 요구되었다고 하자. 하지만 실행까지에 필요한 메모리 공간(Heap영역, Stack 영역, 코드, 데이터)의 합이 40KB 라면, 실제 물리 메모리에는 40KB 만 올라가 있고, 나머지 60KB 만큼은 필요시에 물리메모리에 요구한다고 이해할 수 있겠다.
![](https://images.velog.io/images/kcwthing1210/post/6aa92fb6-9c39-46dd-9088-bb01749d199e/image.png)

그리고 특정 가상 주소가 어느 물리 소에 매핑되어있는지 알 수 있어야 한다. 이 때 필요한 것이 **MMU**이다.

- MMU(Memory Management Unit): CPU에 코드 실행시, 가상 주소 메모리 접근이 필요할 때, 해당 주소를 물리 주소 값으로 변환해주는 하드웨어 장치
  즉, CPU는 가상 메모리를 다루고, 가상 메모리의 가상 주소에 접근시 MMU하드웨어를 통해 물리 주소로 변환되어 물리 메모리에 접근한다.
  ![](https://images.velog.io/images/kcwthing1210/post/edb81113-da0e-42d8-804e-204fa603285a/image.png)



## 📌 페이징 시스템(paging system)

가상 메모리 시스템을 구현하는 다양한 방법 중 가장 많이 쓰이는 방법이 페이징 시스템이다.

- paging: 크기가 동일한 page로 가상 주소 공간과 이에 매핑되는 물리 주소 공간을 관리하는 것이다.
- page(page frame): 고정된 동일한 크기의 block
- paging table: 프로세스의 PCB에 Page Table 구조체를 가리키는 주소가 있는데 ,이 Page Table에는 물리 메모리에 있는 page frame 번호와 해당 페이지의 첫 물리 주소 정보를 매핑한 표이이다.
  예를 들어, 리눅스에서는 4KB로 paging을 하고, Page Table에 해당 정보를 기록/사용한다.

![](https://images.velog.io/images/kcwthing1210/post/b49f95d6-e75c-437e-b9d1-e0d45eedd68d/image.png)

- p: 가상 메모리의 page 번호
- d: p안에서 참조하는 위치 (페이지 내부 주소; 변위; offset)

paging system에서  해당 프로세스에서 특정 가상 주소를 가지고 어떤 데이터에 접근하고자 하면,

→ page table에 해당 가상 주소와 그 page 번호(p)가 있는지 확인한다.

→ page 번호가 있으면 이와 매핑된 첫 물리 주소(p')를 알아낸다

→ 그러면 페이지 처음부터 얼마 떨어진 위치인지를 알려주는 변위(d)를 더하면

→ p' + d 가 실제 물리 주소가 된다.

## ✔ 종류
### 1) 다중 단계 페이징 시스템
4GB의 프로세스를 모두 페이지로 나눈다면 이 중 당장 사용되지 않는 데이터까지 페이지로 만들어질 것이고 이러면 너무 많은 페이지로 나눠질 것이다. 이렇게 하지 말고 페이징 정보를 단계를 나누어 생성하면 필요없는 페이지는 생성하지 않고 공간 절약이 가능해진다.

![](https://images.velog.io/images/kcwthing1210/post/256def6e-4b78-49e5-ab84-c566cd7a49d2/image.png)


### 2) 페이징 시스템과 공유 메모리
어떤 경우에는 프로세스간 동일한 물리 주소를 가리키게 하여 공간 절약과 메모리 할당 시간을 절약 할 수도 있다.

![](https://images.velog.io/images/kcwthing1210/post/8ed4b97e-cdc0-49cf-95fa-028e04e69cf4/image.png)

## ✔ MMU와 TLB
MMU는 CPU에 코드 실행시, 가상 주소 메모리 접근이 필요할 때, 해당 주소를 물리 주소 값으로 변환해주는 하드웨어 장치이다. 그러면 매번 MMU가 물리 주소를 확인하기 위해 아래 그림과 같이 메모리를 갔다와야하는데 이 과정을 좀 더 효율적으로 할 순 없을까?

이 때 사용되는 것이 TLB이다.

### 1) TLB
TLB(Translation Lookingside Buffer): 최근 물리 주소로 변환된 가상 주소 정보를 저장하여 페이지 정보를 캐쉬할 수 있는 하드웨어

![](https://images.velog.io/images/kcwthing1210/post/69f7cd00-6779-491f-9af7-d60f0f0a3545/image.png)

# 📌 Demand Paging(요구 페이징)

위와 같은 paging system을 사용하면 프로세스에서 나눠진 page를 언제 물리 메모리에 올려놓을지에 대한 정책이 필요하다. 선행 페이징으로 하면 그냥 프로세슬를 실행하자마다 page먼저 다 올려두는 것인데 이것 보다 실제로 필요할 때 page를 메모리에 올리는 것이 좋을 것이다. 이게 demand paging이다.

- Demand Paging: 프로세스의 모든 데이터를 메모리로 적재하지 않고, 실행 중 필요한 시점에서만 메모리로 적재함
  이 때 valid/Invalid bit가 사용된다.

- Invalid: 사용되지 않는 주소 영역인 경우, 페이지가 물리적 메모리에 없는 경우 (valid는 반대)
  처음에는 모든 page가 invalid로 초기화되고, 사용되면 valid로 되는데, address translation시에 invalid bit이라면 page fault가 발생한다.

- page fault:  어떤 페이지가 물리 메모리에 없을 때 발생하는 인터럽트로, page fault가 발생하면 운영체제가 해당 페이지를 물리 메모리에 올려준다.

여기까지의 과정을 앞선 MMU와 TLB에 더해서 도표로 보면, 이러한 과정으로 진행된다.
![](https://images.velog.io/images/kcwthing1210/post/cf965a13-6a28-4c24-b023-6a1b4c2e52f6/image.png)

![](https://images.velog.io/images/kcwthing1210/post/5e13b5f2-9522-476b-b077-a3f2cf8f01bf/image.png)

# 📌 페이지 교체 정책(Page replacement policy)

## ✔ FIFO 페이지 교체
- 가장 간단한 페이지 교체 알고리즘으로 FIFO(first-in first-out)의 흐름을 가진다. 즉, 먼저 물리 메모리에 들어온 페이지 순서대로 페이지 교체 시점에 먼저 나가게 된다는 것이다.

- 장점 : 이해하기도 쉽고, 프로그램하기도 쉽다.
- 단점
    - 오래된 페이지가 항상 불필요하지 않은 정보를 포함하지 않을 수 있다(초기 변수 등)
    - 처음부터 활발하게 사용되는 페이지를 교체해서 페이지 부재율을 높이는 부작용을 초래할 수 있다.
    - Belady의 모순: 페이지를 저장할 수 있는 페이지 프레임의 갯수를 늘려도 되려 페이지 부재가 더 많이 발생하는 모순이 존재한다.

## ✔ 최적 페이지 교체(Optimal Page Replacement)
- Belady의 모순을 확인한 이후 최적 교체 알고리즘에 대한 탐구가 진행되었고, 모든 알고리즘보다 낮은 페이지 부재율을 보이며 Belady의 모순이 발생하지 않는다. 이 알고리즘의 핵심은 앞으로 가장 오랫동안 사용되지 않을 페이지를 찾아 교체하는 것이다. 주로 비교 연구 목적을 위해 사용한다.

- 장점
    - 알고리즘 중 가장 낮은 페이지 부재율을 보장한다.
- 단점
    - 구현의 어려움이 있다. 모든 프로세스의 메모리 참조의 계획을 미리 파악할 방법이 없기 때문이다.
    - LRU 페이지 교체(LRU Page Replacement)
## ✔ LRU: Least-Recently-Used
- 최적 알고리즘의 근사 알고리즘으로, 가장 오랫동안 사용되지 않은 페이지를 선택하여 교체한다.

- 특징
    - 대체적으로 FIFO 알고리즘보다 우수하고, OPT알고리즘보다는 그렇지 못한 모습을 보인다.

## ✔ LFU 페이지 교체(LFU Page Replacement)
- LFU: Least Frequently Used
- 참조 횟수가 가장 적은 페이지를 교체하는 방법이다. 활발하게 사용되는 페이지는 참조 횟수가 많아질 거라는 가정에서 만들어진 알고리즘이다.

- 특징
    - 어떤 프로세스가 특정 페이지를 집중적으로 사용하다, 다른 기능을 사용하게되면 더 이상 사용하지 않아도 계속 메모리에 머물게 되어 초기 가정에 어긋나는 시점이 발생할 수 있다
    - 최적(OPT) 페이지 교체를 제대로 근사하지 못하기 때문에, 잘 쓰이지 않는다.

## ✔ MFU 페이지 교체(MFU Page Replacement)
- MFU: Most Frequently Used
- 참조 회수가 가장 작은 페이지가 최근에 메모리에 올라왔고, 앞으로 계속 사용될 것이라는 가정에 기반한다.

- 특징
  최적(OPT) 페이지 교체를 제대로 근사하지 못하기 때문에, 잘 쓰이지 않는다.



# 🧩 Reference
- https://libertegrace.tistory.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B0%80%EC%83%81-%EB%A9%94%EB%AA%A8%EB%A6%AC%EC%9D%98-%EC%9D%B4%ED%95%B4



#🎁 캐시의 지역성
# 📌 캐시 메모리(Cache Memory)

## ✔ 캐시메모리란?
- 주기억장치에서 자주 사용하는 프로그램과 데이터를 저장해두어 속도를 빠르게 하는 메모리
    -  그러므로 캐시는 주기억장치보다 크기가 작을 수밖에 없다!
    -  캐시 기억장치와 주기억장치 사이에서 정보를 옮기는 것을 사상(Mapping, 매핑)이라고 함

- 속도가 빠른 장치와 느린 장치간의 속도 차에 따른 병목현상을 줄이기 위한 범용 메모리
    - 이를 위해서는 CPU가 어떤 데이터를 원하는지 어느 정도 예측할 수 있어야 한다.
    - 캐시 메모리에 CPU가 이후에 참조할, 필요 있는 정보가 어느 정도 들어있느냐에 따라 캐시의 성능이 좌우되기 때문

- 주기억장치와 CPU사이에 위치
    - 메모리 계층 구조에서 가장 빠른 소자이며, 처리속도가 거의 CPU의 속도와 비슷할 정도의 속도를 가지고 있다.
    - 캐시메모리를 사용하면 주 기억장치를 접근하는 횟수가 줄어들어 컴퓨터의 처리속도가 향상
    - 캐시의 크기는 보통 수십 KByte ~ 수백 KByte

  ![](https://images.velog.io/images/kcwthing1210/post/166fa575-938b-4646-b240-fab74af3e57f/image.png)

# 📌 캐시의 지역성 원리
## ✔ 캐시의 지역성이란?
- 캐시가 효율적으로 동작하려면, 캐시의 적중율(Hit-rate)를 극대화 시켜야 한다.
- 캐시에 저장할 데이터가 지역성(Locality)을 가져야 한다.
- 지역성이란, 데이터 접근이 시간적, 혹은 공간적으로 가깝게 일어나는 것을 의미한다.
- 지역성의 전제 조건으로 프로그램은 모든 코드나 데이터를 균등하게 Access하지 않는다는 특성을 기본으로 한다.
- 즉, 지역성(Locality)이란
  기억장치 내의 정보를 균일하게 Access하는 것이 아닌 어느 한 순간에 특정 부분을 집중적으로 참조하는 특성이다.

## ✔ 지역성(Locality)의 종류

### 1) 시간적 지역성

- 최근에 참조된 주소의 내용은 곧 다음에 다시 참조되는 특성.
- 특정 데이터가 한번 접근되었을 경우, 가까운 미래에 또 한번 데이터에 접근할 가능성이 높은 것
- 메모리 상의 같은 주소에 여러 차례 읽기 쓰기를 수행할 경우,
  상대적으로 작은 크기의 캐시를 사용해도 효율성을 꾀할 수 있다.


### 2) 공간적 지역성
- 대부분의 실제 프로그램이 참조된 주소와 인접한 주소의 내용이 다시 참조되는 특성
- 특정 데이터와 가까운 주소가 순서대로 접근되었을 경우.
  CPU 캐시나 디스크 캐시의 경우 한 메모리 주소에 접근할 때 그 주소뿐 아니라 해당 블록을 전부 캐시에 가져오게 된다.
- 이때 메모리 주소를 오름차순이나 내림차순으로 접근한다면,
  캐시에 이미 저장된 같은 블록의 데이터를 접근하게 되므로 캐시의 효율성이 크게 향상된다.


# 📌 Caching line
언급했듯이 캐시(cache)는 프로세서 가까이에 위치하면서 빈번하게 사용되는 데이터를 놔두는 장소이다. 하지만 캐시가 아무리 가까이 있더라도 찾고자 하는 데이터가 어느 곳에 저장되어 있는지 몰라 모든 데이터를 순회해야 한다면 시간이 오래 걸리게 된다. 즉, 캐시에 목적 데이터가 저장되어 있다면 바로 접근하여 출력할 수 있어야 캐시가 의미 있어진다는 것이다.

그렇기 때문에 캐시에 데이터를 저장할 때 특정 자료구조를 사용하여 묶음으로 저장하게 되는데 이를 캐싱 라인 이라고 한다. 프로세스는 다양한 주소에 있는 데이터를 사용하므로 빈번하게 사용하는 데이터의 주소 또한 흩어져 있다. 따라서 캐시에 저장하는 데이터에는 데이터의 메모리 주소 등을 기록해 둔 태그를 달아놓을 필요가 있다. 이러한 태그들의 묶음을 캐싱 라인이라고 하고 메모리로부터 가져올 때도 캐싱 라인을 기준으로 가져온다. 종류로는 대표적으로 세 가지 방식이 존재한다.

- 직접 매핑(direct Mapping)
    - 주기억장치의 블록들이 지정된 한 개의 캐시 라인으로만 사상될 수 있는 매핑 방법.
    - 간단하고 구현하는 비용이 적게드는 장점이 있지만 적중률이 낮아질 수 있다는 단점이 있다.
- 어소시에이티브 매핑(Associative Mapping)
    - 직접 매핑 방식의 단점을 보완한 방식.
    - 모든 태그들을 병렬로 검사하기 때문에 복잡하고 비용이 높다는 단점이 있어 거의 사용하지 않는다.
- 세트-어소시에이티브 매핑(Set-Associative Mapping)
    - 직접 매핑과 연관 매핑의 장점만을 취한 방식.