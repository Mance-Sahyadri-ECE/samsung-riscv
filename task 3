#include <stdio.h>
#include <stdint.h>

// Function to create an R-Type instruction
uint32_t createInstructionR(uint8_t opcode, uint8_t funct3, uint8_t funct7, uint8_t rs1, uint8_t rs2, uint8_t rd) {
    return (funct7 << 25) | (rs2 << 20) | (rs1 << 15) | (funct3 << 12) | (rd << 7) | opcode;
}

// Function to create an I-Type instruction
uint32_t createInstructionI(uint8_t opcode, uint8_t funct3, uint8_t rs1, uint8_t rd, uint16_t imm) {
    return (imm << 20) | (rs1 << 15) | (funct3 << 12) | (rd << 7) | opcode;
}

// Function to create an S-Type instruction
uint32_t createInstructionS(uint8_t opcode, uint8_t funct3, uint8_t rs1, uint8_t rs2, uint16_t imm) {
    uint8_t imm11_5 = (imm >> 5) & 0x7F;
    uint8_t imm4_0 = imm & 0x1F;
    return (imm11_5 << 25) | (rs2 << 20) | (rs1 << 15) | (funct3 << 12) | (imm4_0 << 7) | opcode;
}

// Function to create a B-Type instruction
uint32_t createInstructionB(uint8_t opcode, uint8_t funct3, uint8_t rs1, uint8_t rs2, uint16_t imm) {
    uint8_t imm12 = (imm >> 12) & 0x1;
    uint8_t imm10_5 = (imm >> 5) & 0x3F;
    uint8_t imm4_1 = (imm >> 1) & 0xF;
    uint8_t imm11 = (imm >> 11) & 0x1;
    return (imm12 << 31) | (imm11 << 7) | (imm10_5 << 25) | (rs2 << 20) | (rs1 << 15) | (funct3 << 12) | (imm4_1 << 8) | opcode;
}

// Function to create a U-Type instruction
uint32_t createInstructionU(uint8_t opcode, uint8_t rd, uint32_t imm) {
    return (imm << 12) | (rd << 7) | opcode;
}

// Function to create a J-Type instruction
uint32_t createInstructionJ(uint8_t opcode, uint8_t rd, uint32_t imm) {
    uint8_t imm20 = (imm >> 20) & 0x1;
    uint8_t imm10_1 = (imm >> 1) & 0x3FF;
    uint8_t imm11 = (imm >> 11) & 0x1;
    uint8_t imm19_12 = (imm >> 12) & 0xFF;
    return (imm20 << 31) | (imm19_12 << 12) | (imm11 << 20) | (imm10_1 << 21) | (rd << 7) | opcode;
}

int main() {
    // Example: Creating an R-Type instruction
    uint32_t rType = createInstructionR(0x33, 0x0, 0x20, 1, 2, 3); // opcode=0x33, funct3=0, funct7=0x20, rs1=1, rs2=2, rd=3
    printf("R-Type Instruction: 0x%08X\n", rType);

    // Example: Creating an I-Type instruction
    uint32_t iType = createInstructionI(0x13, 0x0, 1, 3, 0xFF); // opcode=0x13, funct3=0, rs1=1, rd=3, imm=0xFF
    printf("I-Type Instruction: 0x%08X\n", iType);

    // Example: Creating an S-Type instruction
    uint32_t sType = createInstructionS(0x23, 0x0, 1, 2, 0x1FF); // opcode=0x23, funct3=0, rs1=1, rs2=2, imm=0x1FF
    printf("S-Type Instruction: 0x%08X\n", sType);

    // Example: Creating a B-Type instruction
    uint32_t bType = createInstructionB(0x63, 0x0, 1, 2, 0x1FF); // opcode=0x63, funct3=0, rs1=1, rs2=2, imm=0x1FF
    printf("B-Type Instruction: 0x%08X\n", bType);

    // Example: Creating a U-Type instruction
    uint32_t uType = createInstructionU(0x37, 3, 0x12345); // opcode=0x37, rd=3, imm=0x12345
    printf("U-Type Instruction: 0x%08X\n", uType);

    // Example: Creating a J-Type instruction
    uint32_t jType = createInstructionJ(0x6F, 3, 0x1FFFF); // opcode=0x6F, rd=3, imm=0x1FFFF
    printf("J-Type Instruction: 0x%08X\n", jType);

    return 0;
}
