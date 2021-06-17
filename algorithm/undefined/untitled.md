# 2. Recursion의 응용

00. 명심해야 할 것 

* base case 가 존재해야 함 
* 모든 재귀는 최종적으로 base case 에 도달해야 함 



01. 미로 찿기



* 그림

![](../../.gitbook/assets/image%20%2857%29.png)

* 가정

  * 파란색 : 벽
  * 흰색 : 길 
  * 출구 : n-1, n-1   

* 풀이 방법
  *  현재 위치에서 출구까지 가는 경로가 있으려면,
    * 1\) 현재 위치가 출구이거나 혹은
    * 2\) 이웃한 셀들 중 하나에서  현재 위치를 지나지 않고 출구까지 가는 경로가 있거나    
    * 내가 풀려고 하는 문제를 풀려면, 그 문제 안에 내가 풀려고 하는 작은 문제를 풀면 된다.   
* 예제1,. Decision Problem - 답이 Yes or No 인 문제 

  * 출발점에서 출구까지 경로가 있느냐 없느냐 답하는 문



  * ```java
    boolean findPath(x, y){
        if(x, y) is the exit
        return true;
    
        for each neighbouring cell (x', y') of (x, y) do 
            if(x' , y') is on the path
                if findPath(x', y')
                    return true;
        return false
    }
    ```

![](../../.gitbook/assets/image%20%2868%29.png)

* 여기서 발생할 수 있는 무한반복
  * 옆에서 보면 이전 것이 경로 중 하나이므로,  이 둘 사이를 무한히 반복할 수 있다.  
  * \`따라서 이를 수정하면 다음과 같다. 



* 혹은 다른 방법 - 구현해볼 것 
  * ```java
    boolean findPath(x, y)
        if (x, y) is either on the wall or a visited cell
            return false;
        else if (x, y) is the exit
            return true;
        else 
            mark (x, y) as a visited cell;
            for each neighbouring cell (x', y') of (x, y) do
                if findPath(x', y')
                    return true;
            return false;
    ```
  * 



* 전제 
  * 빨간색 : 길이 없다는 것이 확인된 것 
  * 녹색 : 가본 셀이지만, 경로가 있는지 없는지 판별이 아직 안된것 

![](../../.gitbook/assets/image%20%2858%29.png)

* 코드 
  * ```java
    public static boolean findMazePath(int x, int y){
        if(x<0 || y< 0 || x>=N || y< N ){
            return false;
        }
        if(maze[x][y] != PATHWAY_COLOR[white]){
            return false;
        }
        if(x==N-1 && y==N-1){
            maze[x][y] = PATH_COLOR[green];
            return true;
        }
        maze[x][y] = PATH_COLOR[green];
        if (findMazePath(x-1, y) || findMazePath(x, x+1) || 
            findMazePath(x+1, y) || findMazePath(x, y-1)
        ){
            return true;
        }
        maze[x][y] = BLOCKED_COLOR[Red];
        return false; 
    }

    public static void main(String[] args){
        printMaze();
        findMazePath(0,0);
        printMaze();

    }
    ```
  * 
* 경로 예시 
* 
![](../../.gitbook/assets/image%20%2859%29.png)







02. Counting Cells in a Blob

![](../../.gitbook/assets/image%20%2869%29.png)



* 설 명
  * 입력으로 binary 이미지가 주어짐 
  * 각 픽셀은 background pixel\[흰색\] 이거나  혹은 image pixel \[파란\]
  * 서로 연결된 image pixel 들의 집합을  blob 이라고 부름 
  * **상하좌우** 및 **대각 방향**으로도 연결된 것으로 간주 



* 그림에서의 blob 들 

![](../../.gitbook/assets/image%20%2866%29.png)



* 목표 
  * 입력으로 한 점의 좌표가 주어졌을 때 , 그 점이 속해있는 blob의 크기를 구하는 것





* 입력
  * N\*N 크기의 2차원 그리드 
  * 하나의 좌표   
* 출력
  * 픽셀\(x,y\) 가 포함된 blob 의 크기
  * \(x,y\) 가 어떤 blob 에도 속하지 않는 경우에는 0 



* Recursive Thinking 
  * 현재 이 픽셀이 속한 blob의 크기를 카ㅣ운트하려면 
    * 현재 픽셀이 image color 가 아니라면  0을 반환 
    * 현재 픽셀이 image color 라면 
      * 1 . 현재 픽셀을 카운트한다. 
      * 현재 픽셀이 중복 카운트되는 것을 방지하기 위해  다른 색으로 칠한다. 
      * 현재 픽셀이 이웃한 모든 픽셀들에 대해서  그 픽셀이 속한 blob 의 크기를 카운트해서  카운터에 더해주다. 
      * 카운터를 반환한다.  



* 슈도코드

  * ```java
    if the pixel (x, y) is outside the grid
        the result is 0;
    else if pixel (x, y) is not an image pixel or already counted
        the result is 0;
    else
        set the color of the pixel(x,y) to a red color;
        the result is 1 plus the number of cells in each piece of
        the blob that inclueds a mearest neighbour;
    ```

* 내가 짜본 코드
  * ```java
    public int blob(int[]arr, string[][] result, size, int x, int y){
   
        if(x<0 || x>=size || y<0 || y>=size){
            return 0;
        }
    
        if(result[x][y].equals("visit")){
            return 0;
        }

    
    
        int count = 1;
        result[x][y] = "visit"
    
        count 
            += blob(arr, result, size, x, y-1) 
            + blob(arr, result, size, x+1, y-1) 
            + blob(arr, result, size, x+1, y) 
            + blob(arr, result, size, x+1, y+1) 
            + blob(arr, result, size, x, y+1) 
            + blob(arr, result, size, x-1, y+1) 
            + blob(arr, result, size, x-1, y) 
            + blob(arr, result, size, x-1, y-1);
    
        return count;
        
        
    }
    ```





* 강의 코드 

![](../../.gitbook/assets/image%20%2863%29.png)







03. N Queens 

* 전제
  * N \* N 개의 체스판에 N 개의 말을 놓는다.
  * 이때 하나의 말에서 직선상의 모든 부위에  다른 말이 놓여있으면 안된다.  



* 알 수 있는 것 
  * 가로, 세로, 모두 1개의 말이 존재    
* backtracking
  * 이전까지의 과정으로 돌아가면서 해결하는 ㅇ법    
* 상태공간트리 
  * 

![](../../.gitbook/assets/image%20%2860%29.png)

![](../../.gitbook/assets/image%20%2861%29.png)

* 상태공간 트리
  * **찾는 해를 포함하는 트리**
  * 즉, 해가 존재한다면 그것은 반드시 이 트리의 어떤 한 노드에 해당함 
  * 따라서 이 트리를 체계적으로 탐색하면  해를 구할 수 있음 



* 상태공간 트리의 모든 노드를 탐색할 필요는 없다. 

![](../../.gitbook/assets/image%20%2853%29.png)



* 저 non - promising 보다는 [Infeasible](https://www.merriam-webster.com/dictionary/infeasible) 이 더 어울림 



![](../../.gitbook/assets/image%20%2862%29.png)





* 되추적 기법\[BackTracking\]
  * 상태공간 트리를 깊이 우선 방식으로 탐색하여  해를 찾는 알고리
  * \[깊이 우선 탐색\]이라고도 한다. 



![](../../.gitbook/assets/image%20%2854%29.png)





* 슈도 코드
  * ```java
    //매개변수 : 내가 현재 트리의 어떤 노드에 있는지를 
    // 지정하기 위한 것 
    return-type queens(arguments){
        if non-promising
            report failure and return;
        else if success
            report answer and return;
        else
            visit chioldren recursively; 
    }
    ```
* 
![](../../.gitbook/assets/image%20%2865%29.png)

* level

  * 0부터 시작, 
  * 0은 시작 노드,
  * 1은  그 아래 레벨 노

![](../../.gitbook/assets/image%20%2867%29.png)

![](../../.gitbook/assets/image%20%2856%29.png)

* 단계1 . 리턴타입 

  * boolean의 의미 : 성공이냐 실패



  * ```java
    int[] cols = new int[N+1];
    boolean queens(int level){
        if non-promising
            report failure and return;
        else if success
            report answer and return;
        else
            visit chioldren recursively; 
    }
    ```
  * 

* 단계2. 
  * 현재 도착한 노드가 꽝인지 판별하는 것 
    * 노드가 어떤 경우 non-promising 한 지는 나중에 생
  * * ```java
    int[] cols = new int[N+1];
    boolean queens(int level){
        if (!promising(level))
            return false;
        
        else if success
            report answer and return;
        else
            visit chioldren recursively; 
    }
    ```



* 단계3 
  * 답을 판별하는 기능 추
    * Promising 테스트를 통과했다는 가정 하에  level == N 이면 모든 말이 놓였으므로 성
  * ```java
    int[] cols = new int[N+1];
    boolean queens(int level){
        if (!promising(level))
            return false;
        
        else if (level == N)
            return answer ;
        else
            visit chioldren recursively; 
    }
    ```
  * 



* 단계4 
  *  자식 노드들을 recursive 하게 방문하는 방법 추가

    * ㅇ
    * 

  * ```java

    int[] cols = new int[N+1];
    boolean queens(int level){
        if (!promising(level))
            return false;
        
        if (level == N){
            return answer ;
        }
        ///////////////////////
    
        for(int i=1; i<=N; i++){
            cols[level+1] = i; 
            if(queens(level +1)){
                return true
            }
        }
        return false;
        ////////////////////////
    }
    ```



* 단계5. promising 테스트 구
  * 각 말들 간 충돌 여부 검사
  * level 번째 말이 1 - level-1 번째 말들과 충돌하는지 검

![](../../.gitbook/assets/image%20%2864%29.png)



* 
![](../../.gitbook/assets/image%20%2871%29.png)

![](../../.gitbook/assets/image%20%2872%29.png)

