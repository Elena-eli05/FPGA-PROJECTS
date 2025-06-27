# TRAFFIC LIGHT CONTROLLER

module traffic(
    input clk,
    input rst,
    output reg red,
    output reg yellow,
    output reg green
);

    // Clock divider to slow down 100MHz to ~1Hz (1 sec)
   
    reg [25:0] clk_div;
    reg slow_clk;

    always @(posedge clk or posedge rst) begin
        if (rst) begin
            clk_div <= 0;
            slow_clk <= 0;
        end else begin
            clk_div <= clk_div + 1;
            if (clk_div == 26'd49999999) begin  // Half second high, half low
                clk_div <= 0;
                slow_clk <= ~slow_clk;
            end
        end
    end

    // FSM States: 00 - RED, 01 - GREEN, 10 - YELLOW
   
    reg [1:0] ps;     // Present state
    reg [3:0] timer;  // 4-bit timer

    always @(posedge slow_clk or posedge rst) begin
        if (rst) begin
            ps <= 2'b00;
            timer <= 4'd5;
        end else if (timer == 0) begin
            case (ps)
                2'b00: begin ps <= 2'b01; timer <= 4'd5; end // RED → GREEN
                2'b01: begin ps <= 2'b10; timer <= 4'd2; end // GREEN → YELLOW
                2'b10: begin ps <= 2'b00; timer <= 4'd5; end // YELLOW → RED
                default: begin ps <= 2'b00; timer <= 4'd5; end
            endcase
        end else begin
            timer <= timer - 1;
        end
    end

    // LED Outputs
    always @(*) begin
        red = (ps == 2'b00);
        green = (ps == 2'b01);
        yellow = (ps == 2'b10);
    end

endmodule
