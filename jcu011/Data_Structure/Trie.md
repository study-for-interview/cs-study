# 트라이 (Trie)

문자열을 빠르게 검색(탐색)하기 위한 자료구조 이다.

특정 문자열을 탐색할때 그 길이가 N이라면 **O(N)** 의 시간복잡도로 찾을 수 있다.

빠른 탐색시간을 가지지만 **큰 메모리**를 필요로 하는 단점이 있다.


<br> <br> 


## 트라이 예시

아래의 그림은 아래의 문자열 집합에서의 트라이 예시이다.

* **문자열 집합** = {"AE" , "ATV", "ATES", "ATEV", "DE" ,"DC"}

<img src="https://t1.daumcdn.net/cfile/tistory/2521FE4C58955E7532" alt="img" style="zoom: 67%;" />

[출처](https://jason9319.tistory.com/129)



<br> <br> 

### 트라이의 구현 (C++)

연결리스트로 구현한 형태이다.

```cpp
const int MAX_N = 10000;
const int TrieNode = 10; // 트라이 노드의 포인터개수
// ex1) 문자열이 전화번호라면 10 (0~9)
// ex2) 문자열이 소문자 알파벳이라면 26 (a to z)

struct Trie {
    Trie *next[TrieNode];
    bool finish; // 끝나는 지점 표시
    Trie(){
        finish = false;
        memset(next, 0, sizeof(next));
    }
    ~Trie(){
        for(int i=0; i<TrieNode; i++)
            if(next[i]) delete next[i];
    }

    void insert(const char* key){
        if(*key=='\0') finish = true;
        else {
            int cn = *key-'0';
            if(next[cn]==NULL) next[cn] = new Trie();
            next[cn]->insert(key+1);
        }
    }

    // 문제마다 다름
    bool find(const char* key){        
        if(*key == '\0') return false;
        if(finish==true) return true;
        
        int cn = *key-'0';
        return next[cn]->find(key+1);
    }

};
```



<br> <br> 

## 트라이 문제 풀이

* 백준 5052번 - [전화번호 목록](https://www.acmicpc.net/problem/5052)

~~~cpp
#include<bits/stdc++.h>
using namespace std;

const int MAX_N = 10000;
const int TrieNode = 10;

struct Trie {
    Trie *next[TrieNode];
    bool finish;
    Trie(){
        finish = false;
        memset(next, 0, sizeof(next));
    }
    ~Trie(){
        for(int i=0; i<TrieNode; i++)
            if(next[i]) delete next[i];
    }

    void insert(const char* key){
        if(*key=='\0') finish = true;
        else {
            int cn = *key-'0';
            if(next[cn]==NULL) next[cn] = new Trie();
            next[cn]->insert(key+1);
        }
    }

    bool find(const char* key){        
        if(*key == '\0') return false;
        if(finish==true) return true;
        
        int cn = *key-'0';
        return next[cn]->find(key+1);
    }

};

int T,N;
char m[MAX_N+1][TrieNode+1]{};
Trie *root;

int main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0);

    cin>>T;
    while(T--){
        cin>>N;
        root = new Trie;
        for(int i=0; i<N; i++) cin>>m[i];
        for(int i=0; i<N; i++) root->insert(m[i]);

        int chk=0;
        for(int i=0; i<N; i++){
            if(root->find(m[i])){
                chk = 1;
                break;
            }
        }

        if(chk) cout<<"NO"<<'\n';
        else cout<<"YES"<<'\n';

        delete root;
    }
}
~~~





