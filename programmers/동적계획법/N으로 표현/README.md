import java.util.*;
class Solution {
    ArrayList<Integer> cnt_list = new ArrayList<>();
    int answer = -1;
    public int solution(int N, int number) {
        expressionHelper(N, 0, 0, number);			
		
		return answer;
    }
    public void expressionHelper(int N, int count, int result, int number) {
		int temp = N;		
		if(count>8) return;
		if(result==number) {
			if(answer==-1 || answer>count){
                answer = count;
            }
			return;
		}
		for(int i=0; i<8-count; i++) {
			expressionHelper(N, count+i+1, result + temp, number);
			expressionHelper(N, count+i+1, result - temp, number);
			expressionHelper(N, count+i+1, result * temp, number);
			expressionHelper(N, count+i+1, result / temp, number);
			
			temp = extendNumber(temp, N);
		}
	}
	
	public int extendNumber(int result, int N) {
		return result*10 + N;
	}
}