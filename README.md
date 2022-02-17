# weapon-esp-external
 join discord server https://discord.com/invite/B6xbr4r8Ze
 ----------------------------------------
ud (weapon esp external) by Clix#0001 XD
GetNameFromFName
----------------------------------
```
Clix — 10.02.2022
std::string GetNameFromFName(int key)
{
    uint32_t ChunkOffset = (uint32_t)((int)(key) >> 16);
    uint16_t NameOffset = (uint16_t)key;
 
    uint64_t NamePoolChunk = RPM<uint64_t>((uintptr_t)moduleBase + 0xB6528C0 + ((ChunkOffset + 2) * 8)); // ERROR_NAME_SIZE_EXCEEDED
    uint64_t entryOffset = NamePoolChunk + (DWORD)(2 * NameOffset);
    uint16_t nameEntry = RPM<uint16_t>(entryOffset);
 
    int nameLength = nameEntry >> 6;
    char buff[1028];
 
    char* v2 = buff; // rdi
    unsigned __int16* v3; // rbx
    int v4 = nameLength; // ebx
    __int16 result; // ax
    int v6; // edx
    int v7; // ecx
    int v8; // ecx
    __int16 v9; // ax
 
    static DWORD_PTR decryptOffset = NULL;
 
    if (!decryptOffset) 
        decryptOffset = RPM<DWORD_PTR>((uintptr_t)moduleBase + 0xB4F9288);
    
    result = decryptOffset;
 
    if ((uint32_t)nameLength && nameLength > 0)
    {
        read_array(entryOffset + 2, buff, nameLength);
 
        v6 = 0;
        v7 = 38;
 
        do
        {
            v8 = v6++ | v7;
            v9 = v8;
            v7 = 2 * v8;
            result = ~v9;
            *v2 ^= result;
            ++v2;
        } while (v6 < nameLength);
        
 
        buff[nameLength] = '\0';
        return std::string(buff);
    }
    else
    {
        return "";
    }
}
```
gname ^
-------------------------
```

                std::string Names2 = GetNameFromFName(object_id);
                if (exploits::itemesp && Names2.find("PlayerPawn_Athena_Phoebe_C") != std::string::npos)
                {
                    char dist[255];
                    sprintf(dist, E("BOT / AI"));
                    
                    DrawString(15, vRightFootOut.x, vRightFootOut.y , &ESPdistance, true, true, dist);
            
                }
```
