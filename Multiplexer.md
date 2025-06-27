module mux_2x1(
    input a,
    input b,
    input sel,
    output reg y
    );
      
always@(a or b or sel)
begin
    if (sel)
       y=a;
    else
       y=b;
end      
endmodule
