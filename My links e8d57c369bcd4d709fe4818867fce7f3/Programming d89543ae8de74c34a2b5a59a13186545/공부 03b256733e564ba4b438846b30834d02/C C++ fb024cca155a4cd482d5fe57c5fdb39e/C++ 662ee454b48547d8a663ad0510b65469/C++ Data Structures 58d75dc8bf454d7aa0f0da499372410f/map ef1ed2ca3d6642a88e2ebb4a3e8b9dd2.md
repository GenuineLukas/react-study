# map

- 고유한 키를 기반으로 키-값(key-value) 쌍으로 이루어져 있는 정렬된(삽입할 때마다 자동 정렬된) 연관 컨테이너
- [red black](../../Red-Black%20Tree%2049d98c5c7a5d4d0aa133f1e7e0b686fc.md) 로 구현된다. 그렇기 때문에 삽입, 삭제, 수정, 탐색이 O(logN)
- 하나의 키에 중복된 값 불가
- 자동으로 아스키코드순(오름차순) 정렬
- 대괄호 연산자[] 로 직접 참조가능
- find(key)
    - map에서 해당 key를 가진 요소를 찾아 해당 iterator 반환. 만약 없으면 해당 map의 end() 이터레이터 반환.
- **주의점: map의 경우 해당 인덱스에 참조만 해도 맵의 요소가 생긴다. 요소가 없다면 0 또는 빈문자열로 초기화 되어 할당(int 는 0, char은 빈 문자열). ex) key 값으로 0을 갖고 있지 않은 상태에서 mp[0]을 할 경우 순간 0이 할당된다.
    
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    map<string, int> mp;
    string a[] = {"박제욱", "최주형", "전승일"};
    int main() {
      for(int i=0; i<3; i++){
        mp.insert({a[i], i+1});
        mp[a[i]] = i + 1;
      }
      //만약 mp에 해당 키가없으면 0으로 초기화 되어 할당 됨.(int의 경우)
      //만약 mp에 해당 키가없는지 확인하고 싶고
      //초깃값으로 0으로 할당되지 않아야 되는 상황이라면
      //find를 쓰자
      cout << mp["lukas"] << "\n"; //0
      mp["lukas"] = 4;
      cout << mp.size() << "\n"; //4
      mp.erase("lukas");
      auto it = mp.find("lukas");
      if(it == mp.end()){
        cout << "못찾겠다 꾀꼬리\n"; //못찾겠다 꾀꼬리
      }
      mp["lukas"] = 100;
    
      it = mp.find("lukas");
      if(it != mp.end()){
        cout << (*it).first << " : " <<(*it).second << "\n"; //lukas:1    
      }
      for(auto it : mp){
        cout << (it).first << " : " << (it).second << '\n';
      }
      /*
      lukas : 100
      박제욱 : 1
      전승일 : 3
      최주형 : 2
      */
      for(auto it = mp.begin(); it != mp.end(); it++){
        cout << (*it).first << " : " << (*it).second << "\n";
      }
      /*
      lukas : 100
      박제욱 : 1
      전승일 : 3
      최주형 : 2
      */
      mp.clear();
      return 0;
    }
    ```
    
- 맵에 요소가 있는지 없는지 확인하고 요소를 할당하는 로직
    
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    map<int, int> mp;
    int main(){
      if(mp[0] == 0){
        mp[0] = 2;
      } 
      for(auto it : mp) cout << it.first << " " << it.second << "\n"; // 0 2
      return 0;
    }
    ```
    
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    map<int, int> mp;
    int main(){
      if(mp.find(0) == mp.end()){
        mp[0] = 2;
      } 
      for(auto it : mp) cout << it.first << " " << it.second << "\n"; // 0 2
      return 0;
    }
    ```