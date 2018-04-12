# UnderSandofGame_Calssic

```
int setflagstatement1 = 0, setflagstatement2 = 0;;  // 각 상황별 solveMazeUtil 의 재귀에서 이전 단계로 돌아가기 위한 플래그를 세워주는 변수이다. row로 +1 이동하였을 때 setflagstatement1 를 101로 세우고 column으로 이동하였을 때 setflagstatement2를 202로 세워준다.

bool solveMazeUtil(Map maze, int r, int c, Map path, int N, int length)
{
	time_check(); // DO NOT REMOVE OR MOVE THIS STATEMENT

	// if ( current position is goal) return true  목적지에 도착하면 true 를 반환한다.
	if (r == N - 1 && c == N - 1) // 미로의 우측 하단 부분
	{
		path[r][c] = 1; // 목적지에 도착했으니 path에다가 1을 마킹해준다.
		//If you want to save your path temporarily, copy your path into another one, like below.            당신의 경로를 일시적으로 저장하고 싶을시 path를 다른 복사본에다가 저장하여라. 아래와 같이.
		//copy_map(path, answerPath, N);
		return true; // 도착시 ture를 반환하며 재귀를 종료한다. 그러니까 이 if문은 우선적으로 실행되어야 한다.
	}
	// Check if maze[r][c] is valid
	if (isSafe(maze, r, c, path, N) == true) // isSafe함수를 통하여 갈수 있다면 true가 되서 안의 내용이 또 실행되므로 재귀가 재귀를 호출하며 재귀가 반복된당ㅋ
	{                                            //쉽게 생각하자 row 나 column중 하나에다가  +1 을 해서 검사 후 계속 돌고 도는 것이다. 다만 현재는 돌다가 막힌 경우 되돌아 갈 수 없는 상태에 있다.
		// mark r,c as part of solution path
		path[r][c] = 1;
		/* [1] Try to move upward in rows */
		if (solveMazeUtil(maze, r + 1, c, path, N, length + 1) == true)  //재귀적으로 탐색하여 현 위치에다가 row+1을 주어 탐색하는 것이다. 그리고 그 값이 true일 경우 ~~~~를 하고 true 를 반환함. 
		{
			setflagstatement1 = 101;
			return true;
		}
		//when no paths in upward..
		/* [2] Try to move rightward in columns */
		if (solveMazeUtil(maze, r, c + 1, path, N, length + 1) == true) //재귀적으로 탐색하여 현 위치에다가 column+1을 주어 탐색하는 것이다. 그리고 그 값이 true일 경우 ~~~~를 하고 true 를 반환함. 
		{
			setflagstatement2 = 202;
			return true;
		}
		/* If none of the above movements work then BACKTRACK:                        위의 if문들에서 걸리지 않을 경우에는 갈 경로가 없다고 판단되므로 path[r][c] = 1로 설정되었던 것을 path[r][c] = 0으로 재설정하고 뒤로 돌아간다.
		unmark r,c as part of solution path */
		path[r][c] = 0;  // 갈 경로가 없다고 판단됬으니 이 경로또한 막힌 경로이다.
	}

	if (setflagstatement1 == 101) {   /*row 방향으로 한 번 재귀를 돌게 되면 setflagstatement는 101로 설정이 되며
									   이렇게 한번 재귀를 돌고 나서 갈 수 있는 방향에 대하여 isSafe에서 그 이동을 허락하지 않으면 False가 return 되고 이 else if 구문으로 들어오게 된다.
									   그렇게 되면 r+1된 상태에서 false가 return 되었으므로 maze[r][c]에서 한걸음 뒤로 물러나도록 만든다.
									   */
		maze[r][c] = 1;
		r--;
		length--;
	}
	if (setflagstatement2 == 202){    /*column 방향으로 한 번 재귀를 돌게 되면 setflagstatement는 202로 설정이 되며
									   이렇게 한번 재귀를 돌고 나서 갈 수 있는 방향에 대하여 isSafe에서 그 이동을 허락하지 않으면 False가 return 되고 이 else if 구문으로 들어오게 된다.
									   그렇게 되면 r+1된 상태에서 false가 return 되었으므로 maze[r][c]에서 한걸음 뒤로 물러나도록 만든다.(length 를 1 줄인다)
									   */
		maze[r][c] = 1;
		c--;
		length--;
	}

	return false;
}
```
