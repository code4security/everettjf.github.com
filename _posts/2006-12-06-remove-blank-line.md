---
layout: post
title: "去除文章中的多余空行的c++代码（我的作品哦）"
excerpt: "很久以前的C++代码"
tags: [随笔]
date: 2006-12-06
modified: 
comments: true
---

~~~c
//kickspace.cpp
//Using this file ,you can kick out the spaces(enter) in a file (eg. *.txt).
//powder by Everett.
//2006-11-22

#include <cstdlib>
#include <string.h>
#include <iostream>
#include <fstream>
#include "require.h"

using namespace std;

int main(int argc, char *argv[])
{  
    cout<<"Using this program(powdered by Everett) ,\n you can kick out the spaces(enter) in a file (eg. *.txt)."<<endl;
    //argument checking
    if(argc!=2){
                cout<<"Error of arguments' number!"<<endl;
                cout<<"You should specify only one file name(including the extention)"<<endl;
                exit(1);
                }
    //getting and creating the targer file
    ifstream intarget(argv[1]);//get the file for reading
             assure(intarget,argv[1]);
    //calculate the output file name with strcat function
    char outfilename[50];
    char *addWords="TARGET";
    strcpy(outfilename,addWords);
    strcat(outfilename,argv[1]);
        
    ofstream outtarget(outfilename);//show the file ,for writing
             assure(outtarget,outfilename);
    string bufferout;
    
    while(getline(intarget,bufferout)){
                                       if(bufferout=="")continue;
                                       outtarget<<bufferout<<"\n";
                                       }
    cout<<"Ok! \nNow you can find the file called "<<outfilename<<"\n in the same directory."<<endl;
    cout<<"Thanks for using! Bye!"<<endl;
      
    
    //system("PAUSE");
    return EXIT_SUCCESS;
}

//////////////////用了thinking in c++ 中的一个头文件////////////////////

//: :require.h
// From Thinking in C++, 2nd Edition
// Available at http://www.BruceEckel.com
// (c) Bruce Eckel 2000
// Copyright notice in Copyright.txt
// Test for error conditions in programs
// Local "using namespace std" for old compilers
#ifndef REQUIRE_H
#define REQUIRE_H
#include <cstdio>
#include <cstdlib>
#include <fstream>
#include <string>

inline void require(bool requirement, 
  const std::string& msg = "Requirement failed"){
  using namespace std;
  if (!requirement) {
    fputs(msg.c_str(), stderr);
    fputs("\n", stderr);
    exit(1);
  }
}

inline void requireArgs(int argc, int args, 
  const std::string& msg = 
    "Must use %d arguments") {
  using namespace std;
   if (argc != args + 1) {
     fprintf(stderr, msg.c_str(), args);
     fputs("\n", stderr);
     exit(1);
   }
}

inline void requireMinArgs(int argc, int minArgs,
  const std::string& msg =
    "Must use at least %d arguments") {
  using namespace std;
  if(argc < minArgs + 1) {
    fprintf(stderr, msg.c_str(), minArgs);
    fputs("\n", stderr);
    exit(1);
  }
}
  
inline void assure(std::ifstream& in, 
  const std::string& filename = "") {
  using namespace std;
  if(!in) {
    fprintf(stderr, "Could not open file %s\n",
      filename.c_str());
    exit(1);
  }
}

inline void assure(std::ofstream& out, 
  const std::string& filename = "") {
  using namespace std;
  if(!out) {
    fprintf(stderr, "Could not open file %s\n", 
      filename.c_str());
    exit(1);
  }
}
#endif // REQUIRE_H 
~~~
