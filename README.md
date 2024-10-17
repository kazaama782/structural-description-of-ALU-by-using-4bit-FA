# structural-description-of-ALU-by-using-4bit-FA

`timescale 1ns / 1ps

module ALU(Z,X,Y,sign,zero,carry,parity,overflow);
input [15:0]X;
input [15:0]Y;
output [15:0]Z;
output sign,zero,carry,parity,overflow;
wire [3:0]cin;
assign sign =Z[15];
assign zero =~|Z;
assign parity = ~^Z;
assign overflow = (X[15]&Y[15]&~Z[15])|(~X[15]&~Y[15]&Z[15]);
FA mo(Z[3:0],cin[1],X[3:0],Y[3:0],1'b0);
FA m1(Z[7:4],cin[2],X[7:4],Y[7:4],cin[1]);
FA m2(Z[11:8],cin[3],X[11:8],Y[11:8],cin[2]);
FA m3(Z[15:12],carry,X[15:12],Y[15:12],cin[3]);
endmodule

module FA(s,cout,a,b,c);
input [3:0]a;
input [3:0]b;
input c;
output cout;
output [3:0]s;
assign{cout,s}=a+b+c;
endmodule
