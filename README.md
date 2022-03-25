# CRC-16-MODBUS
for just calculate modbus crc 16


//create new project on visual studio console application then clear main code and paste the code







#include <stdio.h>
int main()
{
    unsigned short temp = 0xffff;//init temp
    unsigned short buffer = 0;
    unsigned char input[6] = { 0x01, 0x03, 0x00, 0x00, 0x00, 0x03 };
    for (int i = 0; i < sizeof(input); i++)
    {
        temp = input[i] ^ temp;//XOR gate
        for (int j = 0; j < 8; j++)//for 1 byte 8 bit
        {
            if (temp & 0x01) 
            {
                temp = temp >> 1;
                temp = temp ^ 0xA001;
            }
            else {
                temp = temp >> 1;
            }
        }
    }
    //CRC byte position change
    buffer = temp >> 8; 
    buffer = buffer | (temp << 8);
    printf("CRC: %X\n", buffer);
    return 0;    
}
