DFS

DFS는 깊이 우선 탐색(depth-first-search)의 약자이다. DFS와 BFS는 모두 그래프의 두 가지 탐색 알고리즘 이므로 이를 이해하기 위해서는 그래프 자료구조에 대한 이해가 우선이다.

그래프(graph)의 가장 기본적인 정의는 정점(vertex)와 간선(edge)의 집합이다. 간선은 두 정점을 이어주는 역할을 한다. 자기 자신을 가리킬 수도 있고, 간선에 방향이 있기도 하고 없기도 하며, 가중치가 있기도 하고 없기도 하는 등 매우 다양한 형태의 그래프가 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3bfef670-0ad7-43cd-92b3-10e739cf83de/Untitled.png)

위와 같은 구조가 가장 기본적인 형태의 그래프이다. 정점의 집합을 보통 대문자 **V**로 표기한다. V={1, 2, 3, 4, 5, 6}과 같이 표기할 수 있다. 간선의 집합은 대문자 **E**로 표기한다. 각 간선은 간선의 양 끝 점의 정점의 쌍으로 표기한다. E = {(1, 2), (1, 5), (2, 3), (2, 5), (3, 4), (4, 5), (4, 6)}이다.

V와 E는 집합이므로 그 크기 또한 집합에 절댓값 기호를 씌워서 표현할 수 있다.

여기서는 **|V| = 6**, **|E| = 7이다**.

또한 각 정점마다 **차수**(degree)가 존재하는데 이는 그 정점과 이어진 간선의 개수를 말한다. 1번 정점의 차수는 2, 5번 정점의 차수는 3... 이런 식.

정점은 **노드**(node)라고도 흔히들 부름.

다양한 종류의 그래프가 있지만 이 글에서는 배보다 배꼽이 커지는 것 같아서 생략하고 다른 글에서 정리함.

2차원 배열에서의 DFS 구현

```cpp
#include <bits/stdc++.h>
using namespace std;
#define X first
#define Y second
int board[502][502] =
    {{1, 1, 1, 0, 1, 0, 0, 0, 0, 0},
     {1, 0, 0, 0, 1, 0, 0, 0, 0, 0},
     {1, 1, 1, 0, 1, 0, 0, 0, 0, 0},
     {1, 1, 0, 0, 1, 0, 0, 0, 0, 0},
     {0, 1, 0, 0, 0, 0, 0, 0, 0, 0},
     {0, 0, 0, 0, 0, 0, 0, 0, 0, 0},
     {0, 0, 0, 0, 0, 0, 0, 0, 0, 0}};  // 1이 파란 칸, 0이 빨간 칸에 대응
bool vis[502][502];                    // 해당 칸의 방문 여부 저장 처음에는 전부 0
int n = 7, m = 10;                     // board의 행과 열의 크기
int dx[4] = {1, 0, -1, 0};
int dy[4] = {0, 1, 0, -1};  // 상하좌우 네 방향을 나타네는 방향벡터(x가 행, y가 열을 나타냄)

int main(void) {
  ios_base::sync_with_stdio(0);
  cin.tie(0);
  stack<pair<int, int> > S;
  vis[0][0] = 1;
  S.push({0, 0});
  while (!S.empty()) {
    pair<int, int> cur = S.top();
    S.pop();
    cout << "(" << cur.X << ", " << cur.Y << ") -> ";
    for (int dir = 0; dir < 4; dir++) {
      int nx = cur.X + dx[dir];
      int ny = cur.Y + dy[dir];
      if (nx < 0 || nx >= n || ny < 0 || ny >= m) continue;
      if (vis[nx][ny] || board[nx][ny] != 1) continue;
      vis[nx][ny] = 1;
      S.push({nx, ny});
    }
  }
}
```
