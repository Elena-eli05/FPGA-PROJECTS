module comp_4(A_gt_B,A_lt_B,A_eq_B,A,B);

input [3:0]A;
input [3:0]B;
output reg A_gt_B,A_lt_B,A_eq_B;

always@(A or B) begin
  A_gt_B=0;
  A_lt_B=0;
  A_eq_B=0;
     
        if (A>B)
            A_gt_B=1;
        else if (A<B)
            A_lt_B=1;
        else 
            A_eq_B=1;
    end       

endmodule
