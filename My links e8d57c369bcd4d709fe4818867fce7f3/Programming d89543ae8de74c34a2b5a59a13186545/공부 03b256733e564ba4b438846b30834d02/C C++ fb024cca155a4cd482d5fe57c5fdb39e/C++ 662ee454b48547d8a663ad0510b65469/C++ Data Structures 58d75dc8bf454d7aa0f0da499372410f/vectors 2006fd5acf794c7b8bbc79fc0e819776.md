# vectors

- 동적 배열
- 컴파일 시점에 시범에 사용해야 할 요소들의 개수를 모른다면 써야 함
- 연속된 메모리 공간에 위치한 같은 타입의 요소들의 모음
- 숫자인덱스 기반
- 중복을 허용
- O(1): 탐색 & 맨 앞뒤 요소 삭제
- O(n): 맨 앞뒤 아닌요소 삭제 삽입
- push_back(), pop_back(), erase(), find(from, to , value), clear(), fill(from, to , value)

```cpp
#include<bits/stdc++.h>
using namespace std;
vector<int> v;
int main(){
  for(int i = 1; i<= 10; i++) v.push_back(i);
  for(int a : v) cout << a << " "; // 1 2 3 4 5 6 7 8 9 10
  cout << "\n";
  v.pop_back();

  for(int a: v) cout << a << " "; // 1 2 3 4 5 6 7 8 9
  cout << "\n";

  v.erase(v.begin(), v.begin() + 3); 

  for(int a : v) cout << a << " "; // 4 5 6 7 8 9
  cout << "\n";

  auto a = find(v.begin(), v.end(), 100);
  if(a == v.end()) cout << "not found" << "\n"; //not found

  fill(v.begin(), v.end(), 10);
  for(int a : v) cout << a << " ";// 10 10 10 10 10 10
  cout << "\n";
  v.clear();
  cout << "아무것도 없을까?\n"; // 아무것도 없을까?
  cout << "\n";
  for(int a : v) cout << a << " ";
  cout << "\n";
  return 0;
}
```

### 벡터의 정적할당

vector라고 해서 무조건 크기가 0인 빈 vector를 만들어 동적할당으로 요소를 추가하는 것은 아니다. 애초에 크기를 정해놓거나 해당 크기에 대해 어떠한 겂으로 초기화 해놓고 시작할 수도 있다.

- 5개의요소를 담을 수있는 vector를 선언, 모든 값을 100으로 채우기
    
    ```cpp
    #include<bits/stdc++.h>
    using namespace std;
    vector<int> v(5, 100);
    int main(){
      for(int a: v) cout << a << " ";
      cout << "\n"; //100 100 100 100 100 
      return 0;
    }
    ```
    
- alternatives
    
    ```cpp
    #include<bits/stdc++.h>
    using namespace std;
    vector<int> v{10, 20, 30, 40, 50};
    int main(){
      ios_base::sync_with_stdio(false);
      cin.tie(NULL);
      cout.tie(NULL);
      for(int i : v){
        cout << i << " " ; //10 20 30 40 50
      }
      return 0;
    }
    ```
    

### 2차원 배열

총 3가지 방법

```cpp
#include<bits/stdc++.h>
using namespace std;
vector<vector<int>> v;
vector<vector<int>> v2(10, vector<int>(10, 0));
vector<int> v3[10];

int main() {
  for(int i = 0; i<10; i++){
    vector<int> temp;
    v.push_back(temp);
  }
  return 0;
}
```