# CRC-16-MODBUS
for just calculate modbus crc 16


//create new project on visual studio console application then clear main code and paste the code





#include <stdio.h>
unsigned char input[6] = { 0x01, 0x03, 0x00, 0x00, 0x00, 0x03 };//request packet

unsigned int fnxCrc(unsigned char* input, int len)
{
    unsigned int temp = 0xFFFF;//init temp
    unsigned int buffer = 0;    
    for (int i = 0; i < len; i++)
    {
        temp = input[i] ^ temp;//XOR gate
        for (int j = 0; j < 8; j++)//for 1 byte 8 bit
        {
            if (temp & 0x01)
            {
                temp = temp >> 1;
                temp = temp ^ 0xA001;
            }
            else
            {
                temp = temp >> 1;
            }
        }
    }
    //CRC byte position change
    buffer = temp >> 8;
    buffer = buffer | temp << 8 ;
    buffer = buffer >> 8;
    return buffer;
}

int main()
{
    int x = fnxCrc(input, 6);
    printf("CRC: %X\n", x);
}
