	
1. Return the first Non-repeating in the array of string
2. Return List<String>  longest word from Dictionary.  LongestWord(String letters, Dictionary dict)


Learning:

* Count array should be integer of length 256, bcs we have 256 character.
* (int) char: char convert to integer as a representation of ascii
* (char) : for printing use this.
* Any string or character, you are compairing if its matches the do something -> do that once loop completes.
* Any string or character, if not matching then break it, dont have to go ahead with compairing more.
* Use Set to remove duplicate.
* LinkedHashMap - store order of insertion

```
import java.util.*;

class Dictionary{

    private String []entries;

    public Dictionary(String[] entries) {
        this.entries = entries;
    }
    public String[] getDictionary(){
        return this.entries;
    }

}

public class Solution {
    public static Set<String> getLongestWord(String letters, Dictionary dict){
//        List<String> result = new ArrayList<>();
        Set<String> set = new HashSet<String>();

        int count[] = new int[256];
        for(int i=0; i<letters.length();i++){
            count[(int) letters.charAt(i)]++;
        }

        for(int i=0; i<count.length; i++){
            if(count[i] == 1)
            System.out.println(count[i]+" : "+ (char) i);
        }
        int i = 0;
        int max = 0;
        String val = null;

        for(String s: dict.getDictionary()){

            for(i=0; i<s.length(); i++){
                if(count[(int) s.charAt(i)] != 1){
                    break;
                }
            }
            if(i == s.length()){
                if(i == max){
                    set.add(val);
                    set.add(s);
                }
                if(i > max){
                    max = i;
                    val = s;
                }
            }

        }


        return set;
    }
    public static void main(String []args){
        Dictionary dict = new Dictionary(new String[] {"to","toe", "toes", "dogs","books","banana"});
        Set<String> res = getLongestWord("osetdg", dict);

        Iterator itr = res.iterator();
        while(itr.hasNext()){
            System.out.println(itr.next());
        }
    }
}
```