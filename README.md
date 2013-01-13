colordetection
==============
// ColorDetection.cpp : Defines the entry point for the console application.
//

#include "stdafx.h"
#include <opencv/highgui.h>
#include <opencv/cv.h>
#include <iostream>

using namespace std;


int main()
{
  char name[] = "deteksiwarna.jpg";
	IplImage* src = cvLoadImage(name,1);
	IplImage* copy = cvCreateImage(cvGetSize(src),8,3);
	CvScalar s,c;
	cout<<"Searching green color ... \n";

	for(int i=0;i<(src->height);i++)
	{
		for(int j=0;j<(src->width);j++)
		{
			s = cvGet2D(src,i,j);
			if((s.val[2]<100)&&(s.val[1]<100)&&(s.val[0]<50))
			{
				c.val[2]=0;
				c.val[1]=0;
				c.val[0]=0;
				cvSet2D(copy,i,j,c);
			}
			else
			{
				c.val[2]=255;
				c.val[1]=255;
				c.val[0]=255;
				cvSet2D(copy,i,j,c);
			}
		}
	}

	cout<<"colour found ... \n";
	
	cvNamedWindow("input", CV_WINDOW_AUTOSIZE);
	cvShowImage("input", src);
	cvNamedWindow("output", CV_WINDOW_AUTOSIZE);
	cvShowImage("output", copy);
	cvWaitKey();
	cvReleaseImage(&src);

	return 0;
}

