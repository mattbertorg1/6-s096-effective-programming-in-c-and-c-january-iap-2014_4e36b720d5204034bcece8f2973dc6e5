---
course_id: 6-s096-effective-programming-in-c-and-c-january-iap-2014
layout: course_section
parent_title: Assignments
title: Sample Solution to Assignment 1, Problem 2
type: course
uid: 61a02ed5086cd6b81a4bfe6dac8a5beb

---

« [Back to Assignments]({{< baseurl >}}/sections/assignments)

/\*

PROG: floating

LANG: C

\*/

#include <stdio.h>

#include <stdlib.h>

#include <stdint.h>

#include <math.h>

#define ABSOLUTE\_WIDTH 31

#define MANTISSA\_WIDTH 23

#define EXPONENT\_WIDTH 8

#define EXPONENT\_MASK 0xffu

#define MANTISSA\_MASK 0x007fffffu

#define EXPONENT\_BIAS 127

union float\_bits {

 float f;

 uint32\_t bits;

};

void print\_float( FILE \*output, float f ) {

 union float\_bits t; t.f = f;

 uint32\_t sign\_bit = ( t.bits >> ABSOLUTE\_WIDTH );

 uint32\_t exponent = ( t.bits >> MANTISSA\_WIDTH ) & EXPONENT\_MASK;

 uint32\_t mantissa = ( t.bits  &  MANTISSA\_MASK );

 if( sign\_bit != 0 ) {

 fprintf( output, "-" );

 }

 if( exponent > 2 \* EXPONENT\_BIAS ) {

 fprintf( output, "Inf\\n" ); /\* Infinity \*/

 return;

 } else if( exponent == 0 ) {

 fprintf( output, "0." ); /\* Zero or Denormal \*/

 exponent = ( mantissa != 0 ) ? exponent + 1 : exponent;

 } else {

 fprintf( output, "1." ); /\* Usual \*/

 }

 for( int k = MANTISSA\_WIDTH - 1; k >= 0; --k ) {

 fprintf( output, "%d", ( mantissa >> k ) & 1 );

 }

 if( exponent != 0 || mantissa != 0 ) {

 fprintf( output, " \* 2^%d\\n", (int) ( exponent - EXPONENT\_BIAS ) );

 }

}

int main() {

 FILE \*input  = fopen( "floating.in",  "r" ),

 \*output = fopen( "floating.out", "w" );

 size\_t N; float f;

 fscanf( input, "%zu", &N );

 for( size\_t i = 0; i < N; ++i ) {

 fscanf( input, "%f", &f );

 print\_float( output, f );

 }

 fclose( input );

 fclose( output );

 return 0;

}

Below is the output using the test data:

**floating:**

 1: OK \[0.004 seconds\] OK!

 2: OK \[0.004 seconds\] OK!

 3: OK \[0.004 seconds\] OK!

 4: OK \[0.004 seconds\] OK!

 5: OK \[0.005 seconds\] OK!

 6: OK \[0.004 seconds\] OK!

 7: OK \[0.004 seconds\] OK!

  

« [Back to Assignments]({{< baseurl >}}/sections/assignments)