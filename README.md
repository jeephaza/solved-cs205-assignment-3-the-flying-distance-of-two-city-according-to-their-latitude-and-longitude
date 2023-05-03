Download Link: https://assignmentchef.com/product/solved-cs205-assignment-3-the-flying-distance-of-two-city-according-to-their-latitude-and-longitude
<br>
The problem is to calculate the flying distance of two city according to their latitude and longitude. The file with cities’ information is given to us. What we need to do is to make the input more convienient. That is the user only need to input the name of the city, and we can get the latitude and longitude from the file and then calculate the distance between them. Besides, if the user input the incomplete name of the city, the program should give some tips to help the user input the right name of the city. Then, when we get the latitude and the longitude of the city, we can calculate the distance using below methods. If we assume the Earth is a perfect sphere, then we can calculate the distance between them directly by the equation below. (Earth radius: 6371km)

<table width="574">

 <tbody>

  <tr>

   <td width="12"></td>

   <td width="562">


    <table width="554">

     <tbody>

      <tr>

       <td width="554">let phi = 90 – latitude , theta=longitudec  = sin(phi1) * sin(phi2) * cos(theta1-theta2) +cos(phi1) * cos(phi2)d  = R*arccos(c)</td>

      </tr>

     </tbody>

    </table></td>

  </tr>

 </tbody>

</table>

<h2>Part 2-Code</h2>




<table width="588">

 <tbody>

  <tr>

   <td width="588">const int R = 6371; using namespace std; int size;struct info_table{     string name;     string country;     double latitude;     double longitude;};string del_blank(int begin,int end,string str){     while(str[begin]==’ ‘){ begin++; }     while(str[end]==’ ‘){ end–; }     return str.substr(begin,end-begin+1);}bool isDouble(string str){     int count = 0;     if(str[0]==’+’||str[0]==’-‘||(str[0]&gt;=’0’&amp;&amp;str[0]&lt;=’9′)){         for(int i=1;i&lt;str.length();i++){             if(str[i]==’.’) count++;else if(str[i]&gt;=’0’&amp;&amp;str[i]&lt;=’9′) continue;             else return false;             if(count&gt;1) return false;}     }else return false;     return true;}int load(info_table *city){     ifstream file;     file.open(“./world_cities.csv”);     if(!file) return -1;int loc[4],index,count = 0,temp=0;     bool judge = true;     string str;     while(getline(file,str)){         judge = true;         index=-1;temp++;         for(int i=0;i&lt;str.length();i++){             if(str[i]&gt;=’A’&amp;&amp;str[i]&lt;=’Z’) str[i]=str[i]-‘A’+’a’;             if(str[i]==’,’){                 index++;if(index&lt;4) loc[index]=i;                 else {                     judge=false;                     break;}}         }         if(index!=3||!judge){             printf(“Warning:The data of the file is wrong.[Line:%d]
”,temp);             continue;         }string name = del_blank(0,loc[0]-1,str);         string country = del_blank(loc[1]+1,loc[2]-1,str);</td>

  </tr>

 </tbody>

</table>




<table width="588">

 <tbody>

  <tr>

   <td width="588">        string latitude = del_blank(loc[2]+1,loc[3]-1,str);         string longitude = del_blank(loc[3]+1,str.length()-1,str);         if(name.length()&gt;Maxlength||country.length()&gt;Maxlength){printf(“Warning:The length of names is overlong.[Line:%d]
”,temp);             continue;}         if(count&gt;=Arr_size){             printf(“Warning:The size is over the maximum array size
”);             break;}city[count].name = name;         city[count].country = country;         if(isDouble(latitude.c_str())&amp;&amp;isDouble(longitude.c_str())){             double lati = atof(latitude.c_str());             double longti = atof(longitude.c_str());             if(lati&lt;-90||lati&gt;90||longti&lt;-180||longti&gt;180){                 printf(“Warning:The data of the file is wrong.[Line:%d]
”,temp);                 continue;}             else{city[count].latitude = lati;                 city[count].longitude = longti;}         }         else{printf(“Warning:The data of the file is wrong.[Line:%d]
”,temp);             continue;}         count++;}file.close();     return count;}int prompt(info_table *city){     int temp=0,cnt[Arr_size],num;     string str,input;     getline(cin,str);input = del_blank(0,str.length()-1,str);     for(int i=0;i&lt;input.length();i++){if(input[i]&gt;=’A’&amp;&amp;input[i]&lt;=’Z’) input[i]=input[i]+’a’-‘A’;}if(input==”bye”) return -4;     if(input.length()&lt;3) return -1;     for(int i=0;i&lt;size;i++){if(city[i].name.find(input)!=string::npos){             if(city[i].name==input) return i;             else cnt[temp++] = i;}     }     if(temp==1) return cnt[0];     if(temp&gt;1){printf(“Here are the choices, please input the right one!
”);         printf(“*************************************************
”);         for(int i=0;i&lt;temp;i++)printf(“Choice #%d: %s
”,i+1,city[cnt[i]].name.c_str());         printf(“*************************************************
”);</td>

  </tr>

 </tbody>

</table>

<h2>Part 3-Result &amp; Verification</h2>

<strong>Test case #1                                                                                                                                                                              </strong>

Set the maximum length of names to 25, and the array size to 800.

Output: Warning:The data of the file is wrong.[Line:349]

Warning:The length of names is overlong.[Line:418]

Warning:The length of names is overlong.[Line:419]

Warning:The length of names is overlong.[Line:455]

Warning:The length of names is overlong.[Line:486]

Warning:The length of names is overlong.[Line:642]         Warning:The size is over the maximum array size

<strong>Test case #2                                                                                                                                                                              </strong>

<strong>Test case #3                                                                                                                                                                              </strong>

<strong>Test case #4                                                                                                                                                                              </strong>

<strong>Test case #5                                                                                                                                                                              </strong>

<strong>Test case #6                                                                                                                                                                              </strong>

<h2>Part 4-Difficulties &amp; Solutions</h2>

1.Since we need to read the information from the file, we need to use ifstream. In this case, getline() is used.

2.When the name information of the file is overlong, we choose to ignore the data, send a warning and then continue reading the information from the file. When the size of the data is bigger than maximum array size, the program will send a warning and ignore the data below.

3.Since we need to find the relating data in the file, we need to use structure to help us link the information.

4.If we input letter is less than 3 or the program cannot find the city, the program will prompt the user to input again.

5.The program will display some cities which are matched, and prompt user to input the right city names.

6.Since the function sin( ) and cos( ) require a radian rather than a degree, we define a macro to transfer the degree to the radian.

7.Since the distance is a floating-point number, we set its type is double when we define it. And we choose to reserve a decimal when output it.

8.If the user input spaces before or behind the city’s name, we should output the city’s name without spaces, so we choose to delete the spaces after we read the city’s name. Also, sicne the program is case-insensitive, so we transfer all uppercase to the lowercase after we input it.

9.Since the program should exit when the user input”bye”, we need another judgement.

10.If the file’s information is not correct, such as its latitude or longitude is not in the range, the program will report “The data of the file is wrong in Line**”. And also, I set a function to check if the file’s longitude and latitude are number, if the data is not a number such as “5..55”, the program will also give a warning.


