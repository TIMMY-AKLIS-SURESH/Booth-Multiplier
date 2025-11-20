`timescale 1ns / 1ps

module booth_multiplier_tb;

    parameter WIDTH = 8;

    reg  signed [WIDTH-1:0] multiplicand;
    reg  signed [WIDTH-1:0] multiplier;
    wire signed [(2*WIDTH)-1:0] product;

    booth_multiplier #(WIDTH) uut (
        .multiplicand(multiplicand),
        .multiplier(multiplier),
        .product(product)
    );

    initial begin
        $display("Time\tMultiplicand\tMultiplier\tProduct");

        // Test case 1:  5 × 3 = 15
        multiplicand = 5; multiplier = 3; #10;
        $display("%0dns\t%d\t\t%d\t\t%d", $time, multiplicand, multiplier, product);

        // Test case 2:  -5 × 3 = -15
        multiplicand = -5; multiplier = 3; #10;
        $display("%0dns\t%d\t\t%d\t\t%d", $time, multiplicand, multiplier, product);

        // Test case 3:  7 × -2 = -14
        multiplicand = 7; multiplier = -2; #10;
        $display("%0dns\t%d\t\t%d\t\t%d", $time, multiplicand, multiplier, product);

        // Test case 4:  -8 × -4 = 32
        multiplicand = -8; multiplier = -4; #10;
        $display("%0dns\t%d\t\t%d\t\t%d", $time, multiplicand, multiplier, product);

        // Test case 5:  127 × 2 = 254
        multiplicand = 127; multiplier = 2; #10;
        $display("%0dns\t%d\t\t%d\t\t%d", $time, multiplicand, multiplier, product);

        // Test case 6:  -128 × 1 = -128
        multiplicand = -128; multiplier = 1; #10;
        $display("%0dns\t%d\t\t%d\t\t%d", $time, multiplicand, multiplier, product);

        // Test case 7:  Random values
        multiplicand = -45; multiplier = 67; #10;
        $display("%0dns\t%d\t\t%d\t\t%d", $time, multiplicand, multiplier, product);

        $stop; // End simulation
    end

endmodule
