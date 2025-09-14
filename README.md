# day20-strings-rotation-of-each-other
  void computeLPS(string &pat, vector<int> &lps){
     int m = pat.size();
      int len = 0;
      lps[0] = 0;
      int i = 1;
      
      while (i < m){
          if (pat[i] == pat[len]){
          len ++;
         lps[i] = len;
            i++;
      } else {
          if(len != 0){
              len = lps[len - 1];
          } else {
              lps[i] = 0;
               i++;
          }
        }
       }
     }
      
      
      bool kmpSearch( string &txt, string &pat){
          int n = txt.size();
          int m = pat.size();
           vector<int> lps(m , 0);
           computeLPS(pat, lps);
           
           int i = 0 , j = 0;
           while (i < n){
               if(txt[i] == pat[j]){
                   i++;
                   j++;
               }
               if (j == m){
                   return true;
               } else if (i < n && txt[i] != pat[j]){
                   if(j != 0){
                       j = lps[j-1];
                   }
                   else {
                       i++;
                   }
               }
           }
              return false; 
      }
      
  
    
    bool areRotations(string &s1, string &s2) {
    
    if (s1.length() != s2.length())
         return false;
         // concatenate s1 with itself
         string temp = s1 + s1;
           return kmpSearch(temp , s2);
        
    }
