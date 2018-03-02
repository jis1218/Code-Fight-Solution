Some people run along a straight line in the same direction. They start simultaneously at pairwise distinct positions and run with constant speed (which may differ from person to person).
If two or more people are at the same point at some moment we call that a meeting. The number of people gathered at the same point is called meeting cardinality.
For the given starting positions and speeds of runners find the maximum meeting cardinality assuming that people run infinitely long. If there will be no meetings, return -1 instead.
Example
For startPosition = [1, 4, 2] and speed = [27, 18, 24], the output should be
runnersMeetings(startPosition, speed) = 3.
In 20 seconds after the runners start running, they end up at the same point. Check out the gif below for better understanding:
```java
int runnersMeetings(int[] startPosition, int[] speed) {
    int max = 0;
    
    for(int i=0; i<startPosition.length-1; i++){
        for(int j=i+1; j<startPosition.length; j++){
            double time = (double) (startPosition[i]-startPosition[j])/(speed[j]-speed[i]);
            int result = 0;
            System.out.println(time);
            if(time>0){
                for(int k=0; k<startPosition.length; k++){
                    if(startPosition[i]+speed[i]*time == startPosition[k]+speed[k]*time){
                        result++;
                    }
                }
                if(result>max){
                    max = result;
                }                
            }            
        }
    }    
    return max==0?-1:max; 
}
```