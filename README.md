### ripplegen
---
https://github.com/CodeShark/RippleGen/

```cc
// BitcoinUtil.cpp
int64 GetTime()
{
  return time(NULL);
}

void RandAddSeedPerfmon()
{
  RandAddSeed();
  
  static int64 nLastPerfmon;
  if (GetTime() < nLastPerfmon + 10 * 60)
    return;
  nLastPerfmon = GetTime();

#ifdef WIN32
  unsigned char pdata[2500000];
  memset(pdata, 0, sizeof(pdata));
  unsigned long nSize = sizeof(pdata);
  long ret = RegQueryValueExA(HKEY_PERFORMANCE_DATA, "Global", NULL, pdata, &nSize);
  RegCloseKey(HKEY_PERFORMANCE_DATA);
  if (ret == ERROR_SUCCESS)
  {
    RAND_add(pdata, nSize, nSize/100.0);
    memset(pdata, 0, nSize);
  }
#endif
}
```

```
```

```
```


