
## 机试
#### 求平方根
```c
#include <stdio.h>
#include <Math.h>
int main () {
	
	
	double x1,x2;
	float a;
	scanf("%f",&a);
	x2 = 1.0;
	do {
		x1= x2;
		x2 = (x1 + a/x1)/2.0;
	} while(fabs(x1-x2)>=1e-6);
	
	printf("%f",x2);
	return 0;
}
```
#### 十进制2二进制
```c
#include <stdio.h>
int main() {
	int n ,ans[100]={},i=0;
	scanf("%d",&n);
	while(n>0) {
		ans[i++] =  n%2;
		n = n/2;
		
	}
	for(i=i-1;i>=0;i--) {
		printf("%d",ans[i]);	
	}
	
	return 0;
}
```
#### 反序数
```c
#include <stdio.h>
int main() {
	int n,ans = 0;
	scanf("%d",&n); 
	while(n>0) {
		ans = ans*10;
		ans = n%10 + ans;
		n = n/10;
	}
	printf("%d",ans);
	return 0;
}
```
#### 十进制2十六进制
```c
#include <stdio.h>
int main() {
	
	int n,i=0;
	char arr[16] = {'0','1','2','3','4','5','6','7','8','9','A','B','C','D','E','F'} ;
	char ans[100]={};
	
	scanf("%d",&n);
	while(n>0) {
		ans[i++] = arr[n%16];
		n = n/16;
	}
	
	for(i = i-1;i>=0;i--) {
		printf("%c",ans[i]);
	}	
	
	
	return 0;
}
```
#### 十进制2x进制
```c
#include <stdio.h>
int main() {

	int n,x,i=0,w;
	char ans[100];	
	scanf("%d%d",&n,&x);
	while(n>0) {
		w = n%x;
		if(w<10) {
			ans[i++] = w+'0';
		}else {
			ans[i++] = w-10+'A';
			
		}
		n= n/x; 
	}
	
	for(i=i-1;i>=0;i--) {
		printf("%c",ans[i]);
	}
	return 0;
}
```
#### x进制2十进制
```c
#include <stdio.h>
#include <string.h>
int main() {
	
	int x,i;
	char s[100];
	scanf("%s%d",&s,&x);
	int ans = 0;
	int len = strlen(s);
	for(i = 0;i<len;i++) {
		ans = ans*x;
		if(s[i]>= '0' && s[i] <='9') {
			ans = ans + s[i]-'0';
		}else {
			ans = ans + s[i]-'A'+10;
		}
	} 
	printf("%d\n",ans);
	
	return 0;
}
```
#### X进制2Y进制
```c
#include <stdio.h>
#include <string.h>
int main() {
	
	int x,y,i=0,ans=0;
	
	char s[100],out[100];
	
	scanf("%s%d%d",&s,&x,&y);
	int len = strlen(s);
	for(i=0;i<len;i++) {
		ans = ans*x;
		if(s[i]>='0' && s[i] <='9') {
			ans += s[i]-'0';
		}else {
			ans += s[i] -'A'+10;
		}
	}
	int j=0;
	while(ans>0) {
		int w = ans%y;
		if(w<10) {
			out[j++] = w+'0';
		}else {
			out[j++] = w -10+'A';
		}
		ans /= y;
	}
	
	for(j=j-1;j>=0;j--) {
		printf("%c",out[j]);
	}
	
	return 0 ;
}
```
#### X进制2Y进制
#### X进制2Y进制
#### X进制2Y进制
#### X进制2Y进制

