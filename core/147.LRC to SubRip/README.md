During your most recent trip to Codelandia you decided to buy a brand new CodePlayer, a music player that (allegedly) can work with any possible media format. As it turns out, this isn't true: the player can't read lyrics written in the LRC format. It can, however, read the SubRip format, so now you want to translate all the lyrics you have from LRC to SubRip.

Since you are a pro programmer (no noob would ever get to Codelandia!), you're happy to implement a function that, given lrcLyrics and songLength, returns the lyrics in SubRip format.

Example

For

lrcLyrics = ["[00:12.00] Happy birthday dear coder,",
             "[00:17.20] Happy birthday to you!"]
and songLength = "00:00:20", the output should be

lrc2subRip(lrcLyrics, songLength) = [
  "1",
  "00:00:12,000 --> 00:00:17,200",
  "Happy birthday dear coder,",
  "",
  "2",
  "00:00:17,200 --> 00:00:20,000",
  "Happy birthday to you!"
]

```java
String[] lrc2subRip(String[] lrcLyrics, String songLength) {
		
    String pattern = "\\[(\\d{2}):(\\d{2}.\\d{2})\\]\\s?([\\w\\s\\W]*)";
    Pattern patterns = Pattern.compile(pattern);

    ArrayList<String> time = new ArrayList<>();
    ArrayList<String> lyric = new ArrayList<>();

    for(String s : lrcLyrics){
        Matcher matcher = patterns.matcher(s);
        matcher.matches();
        int m = Integer.valueOf(matcher.group(1));
        int h = m/60;
        m = m%60;
        String min = String.format("%02d", m);
        String hour = String.format("%02d", h);
        time.add(hour + ":" + min + ":" + matcher.group(2).replace('.', ',') + "0");
        lyric.add(matcher.group(3));
    }

    String result[] = new String[4*time.size()-1];

    for(int i = 0; i<time.size(); i++){
        result[4*i] = String.valueOf(i+1);
        if(i!=time.size()-1){
            result[4*i+1] = time.get(i) + " --> " + time.get(i+1);
            result[4*i+3] = "";
        }else{
            result[4*i+1] = time.get(i) + " --> " + songLength + ",000";
        }
        result[4*i+2] = lyric.get(i);
    }

    return result;
}
```