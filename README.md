```cpp: problem1_0716.cpp
//problem1_0716.cpp
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>
using namespace std;

int main() {
	vector<char> v;
	vector<int>pick;
	int l, c;
	cin >> l >> c;
	for (int i = 0; i < c; i++) {
		char x;
		cin >> x;
		v.push_back(x);
		pick.push_back(1);
	}
	sort(v.begin(), v.end());
	for (int i = 0; i < l; i++) {
		pick[i] = 0;
	}
	do {
		string s = "";
		for (int i = 0; i < c; i++) {
			if (pick[i] == 0) {
				s = s + v[i];
			}
		}
		int cnt1 = 0;
		int cnt2 = 0;
		for (int i = 0; i < s.size(); i++) {
			if (s[i] == 'a' || s[i] == 'e' || s[i] == 'i' || s[i] == 'o' || s[i] == 'u')
				cnt1++;
			else
				cnt2++;
		}
		if (cnt1 < 1 || cnt2 < 2)
			continue;
		cout << s <<'\n';
	} while (next_permutation(pick.begin(), pick.end()));

}
```

```cpp: problem2_0716.cpp
//problem2_0716.cpp
#include<iostream>
#include<queue>
#include<vector>
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<algorithm>

using namespace std;

#define MAX 100001

int N, K;
bool visit[MAX];

int BFS(int N, int K) {
	queue<pair <int, int>> que;
	que.push(make_pair(N, 0));
	visit[N] = true;

	while (!que.empty()) {
		int Line = que.front().first;
		int time = que.front().second;
		que.pop();

		if (Line == K)	return time;

		if (Line + 1 < MAX && !visit[Line + 1]) {
			que.push(make_pair(Line + 1, time + 1));
			visit[Line + 1] = true;
		}
		if (Line - 1 >= 0 && !visit[Line - 1]) {
			que.push(make_pair(Line - 1, time + 1));
			visit[Line - 1] = true;
		}
		if (Line * 2 < MAX && !visit[Line * 2]) {
			que.push(make_pair(Line * 2, time + 1));
			visit[Line * 2] = true;
		}
	}
}

int main() {
	cin >> N >> K;
	
	cout << BFS(N, K) << endl;
	return 0;
}

```

```cpp: problem3_0716.cpp
//problem3_0716.cpp
#include <algorithm>
#include <iostream>
 
#define MAX 15+1
 
using namespace std;
 
int N;
int time_arr[MAX] = {0};
int profit_arr[MAX] = {0};
int max_val = 0 ;
 
void solve(int now_day, int now_sum, int added_num){
    if(now_day == N + 1 ){
        max_val = max(max_val, now_sum);
        return ;
    } 
    else if (now_day > N + 1){
        max_val = max(max_val, now_sum-added_num);
        return ;
    }

    for ( int i = now_day + time_arr[now_day] ; i <= N + time_arr[now_day] ; i++)
        solve(i, now_sum + profit_arr[now_day] , profit_arr[now_day]);
    
}
 
int main(){
    cin >> N;
    for ( int i = 1 ; i <= N; i++){
        cin >> time_arr[i]  >> profit_arr[i] ;
    }
    
    for ( int i = 1 ; i <= N ; i++)
        solve(i, 0, 0);
    
    cout << max_val;
    return 0;
}
 
```
