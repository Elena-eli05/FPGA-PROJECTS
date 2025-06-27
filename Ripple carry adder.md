module fulladder(S,C,A,B,Cin);

 output S;
 output C;
 input A,B,Cin;

 assign S=A^B^Cin;
 assign C=A&B|A&Cin|B&Cin;
endmodule


module adder_ripple(sum,cout,a,b,cin);

output [3:0]sum;
output cout;
input [3:0]a;
input [3:0]b;
input cin;

wire w1,w2,w3;

fulladder f0(sum[0],w1,a[0],b[0],cin);
fulladder f1(sum[1],w2,a[1],b[1],w1);
fulladder f2(sum[2],w3,a[2],b[2],w2);
fulladder f3(sum[3],cout,a[3],b[3],w3);

endmodule
