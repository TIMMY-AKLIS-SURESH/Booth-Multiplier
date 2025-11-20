// Booth's Algorithm - Signed Multiplier
module booth_multiplier #(
    parameter WIDTH = 8
)(
    input  signed [WIDTH-1:0] multiplicand,
    input  signed [WIDTH-1:0] multiplier,
    output signed [(2*WIDTH)-1:0] product
);
    reg signed [(2*WIDTH):0] acc;   // Accumulator with extra bit for Booth's algorithm
    reg signed [WIDTH-1:0] m;       // Multiplicand register
    reg signed [WIDTH-1:0] q;       // Multiplier register
    reg q_1;                        // Extra bit for Booth's algorithm
    integer i;

    always @(*) begin
        // Initialize
        m     = multiplicand;
        q     = multiplier;
        acc   = { {WIDTH{1'b0}}, q, 1'b0 }; // {A, Q, Q-1}
        q_1   = 1'b0;

        // Booth's algorithm loop
        for (i = 0; i < WIDTH; i = i + 1) begin
            case ({acc[0], q_1})
                2'b01: acc[(2*WIDTH):WIDTH] = acc[(2*WIDTH):WIDTH] + m; 
                2'b10: acc[(2*WIDTH):WIDTH] = acc[(2*WIDTH):WIDTH] - m; 
                default: ; // No operation
            endcase

            // Arithmetic right shift (A, Q, Q-1)
            {acc, q_1} = {acc[2*WIDTH], acc[(2*WIDTH):0], q_1} >>> 1;
        end

        // Final product
        // Remove the extra Q-1 bit and combine A and Q
        // acc[WIDTH-1:0] = Q, acc[(2*WIDTH)-1:WIDTH] = A
    end

    assign product = acc[(2*WIDTH):1]; // Skip Q-1 bit
endmodule
