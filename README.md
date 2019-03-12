# Dynamic-Programming
Longest Increasing Subsequence and Longest Common Subsequence.


#include<bits/stdc++.h>
using namespace std;
void lcs(string s1,string s2)
{
    int n=s1.length();
    int m=s2.length();
    int dp[n+1][m+1];
    for(int i=0;i<=n;i++)
    for(int j=0;j<=m;j++)
    if(i==0||j==0)
    dp[i][j]=0;
    for(int i=1;i<=n;i++)
    for(int j=1;j<=m;j++)
    {
        if(s1[i-1]==s2[j-1])
        dp[i][j]=1+dp[i-1][j-1];
        else
        dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
    }
    cout<<"\n"<<" The length of LCS is "<<dp[n][m]<<"\n";
    int i=n,j=m;
    stack<char> st;
    while(i>0&&j>0)
    {
        if(s1[i-1]==s2[j-1])
        {
            st.push(s1[i-1]);
            i--;j--;    
        }
        else if(dp[i-1][j]>dp[i][j-1])
        i--;
        else
        j--;
                
    }
    cout<<" The LCS is : ";
    while(!st.empty())
    {
        cout<<st.top();
        st.pop();    
    }
    cout<<"\n";
} 
void lis(string s)
{
    int n=s.length();
    int a[n];
    int maxx=INT_MIN;
    for(int i=0;i<n;i++)
    a[i]=1; 
    stack<char> st;
    for(int i=1;i<n;i++)
    {
        for(int j=i-1;j>=0;j--)
        {
            if( (a[j]+1>a[i]) && (s[i]>s[j]) )
            {
                a[i]=a[j]+1;
                
            }
            if(a[i]>maxx)
                maxx=a[i];
            
        }                
        
    }
    cout<<"\n"<<" The length of LIS is "<<maxx<<"\n";
    int temp=maxx;
    for(int i=n-1;i>=0;i--)
    {
        if(a[i]==maxx)
        {
            st.push(s[i]);
            maxx--;
        }
    }
    while(!st.empty())
    {
        cout<<st.top();
        st.pop();
    }
    cout<<endl;
    
}
int main()
{
    string s1;
    string s2;
    cin>>s1;
    cin>>s2;
    lcs(s1,s2);
    lis(s1);
    
return 0;
}
