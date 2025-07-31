---
title: PicoCTF2024 Verify
draft: false
tags:
  - Forensics
---
## Description

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcSTu2xM06rxNAAmTWTkoTvUJpfTeTLfa4DPoN2dcbUiIqsSmwpNmGzPgCltVoNFT9974cH8nSYi1ZIcZ-TeBoam8D7A8Khqyihzl7UR9boDJ1D9SFGquMUShYpZ5f6rmxi_Uad?key=EDQt9HLhdrG6kmd3ep2vsmbc)

## Solution

After SSHing and entering the password, I gained access to their server. I ran the ls command and the following is the output
  
```
ctf-player@pico-chall$ ls

checksum.txt  decrypt.sh  files
```

I went into the files directory to check how many files there were. Below is the output

  
```

ctf-player@pico-chall$ cd files/

ctf-player@pico-chall$ ls

0SgkM1fC  3aMAegi2  7NBIv8bi  A8X4q2Hn  Cwfv60OS  GhwoHV4M  Ka9uxW6u  NB0dzXJg  QcXjRtBd  UCbhwrDb  WzxM1rI6  b8hbdeFv  eRcEh616  kvpk6rIp  nVO17uZV  qIqcOTDP  tmkJMhbV  yTiWOwXD

0aer7B0J  3laJICck  7Snixk9W  ABh1G8a0  DGOlVleK  Gpbebiyr  Kc5sfOun  NHSLSull  Qm0B85oQ  UgDsmf5L  X3z7ayAf  bMcbuEVi  eoW9IJAR  l70cIeRx  npy5LylP  qKIr0SCL  ud4LEsxA  yb3Ro4yS

0b3lt0HK  3mHrLQG2  7eaPaid5  AUijzvDq  DINN9cgG  H6Mlhvd5  KhnreD4t  NYT2nPuv  Qxx5KB3R  V3xeKcD7  X5Vhdb8H  bVoP3eel  fpXvjTBY  l8tB6vEL  nxx3UCp8  qMqcX95Y  uhLtbHVL  ypzAaM0c

0ia8IBYb  3nroY5Wt  7ylewstJ  AWnJiVoE  DNwq8kf8  HS8wBLPJ  L9tRKUkW  NlN25jkt  R84tLxGR  VBHAXd7G  Y4FnPPHX  bZEwUIec  fw6XlbF3  lEjMl22a  oLZldZsM  qfWh95Q9  vQmN5k6y  yzW64294

0uUAy06x  4BRDZhS7  7zsihLxd  AfnUEE9s  Dq8qjJ8S  IMoTEVt4  LZgQIZ9b  NlymPzCl  RKOBoCMd  VM5DLaA2  YEOowfPv  blsMKCvn  g1qINnts  lMIM4IQe  oNfmBvds  rPOS47wB  vQtPAQBH  z1DTGQLy

17iH5ioj  4EqhTV10  8N3DHyAn  AgQhab96  Dr3JaQz7  IjkDI0gL  LnKLtxdL  NrbmwP3r  RSQ5Ynin  VU1Tnx8J  YZc8J6Vf  bnahMLHf  gewOpz6a  lbsGcfLr  oWfAJ9wj  rXWuGW1m  vmLoCSN5  z5y1jgty

1CY2Hque  4Fegg7AZ  8NfqFqEn  AlhLQIGI  Dt7YKSAq  IwVJbP5E  LoSmsO5t  O3c1wd4r  RV6BgBu6  VZqopSEM  YjEaz92U  cO1o2qFY  gr99Nl0G  lbszmcDf  ocTCyt2G  rgZiIAPZ  vt86VpBP  zHpAJtSR

1LPOMJE7  4gMs4KnO  8OpGe3TY  Au8Ov7jr  E1grB9Sb  J7BJ7tAo  MAd4OQmU  OkXybbh3  RWol5Yvg  Vc1VEpYz  YkYjwuGz  cVywfT1b  gru5fnYQ  mDzgzkrP  ocoustRi  rjta4881  vzBdlMd6  zJHj9Wev

1P5dsfLj  4l9DWh5d  8WA32dcd  B8RXEf4S  ETctMG1o  JD0ZwfH8  MBaThKzn  OtnjktH8  RXQH6a3z  Vc6sosw2  ZEEtJ79A  cZXSF7wu  hRF2XNzg  mMNEp8Zi  orQXAz13  ryxNv3Er  w2pqQhei  zQZjRCvK

1Tst6fbt  5HAN1XjT  8WYKhs9b  BMlbLM49  EYaK1nX6  JIPRVMlG  MLDxW9mt  PNNRiq3F  RrQhgxZJ  VhrXhFPH  ZK4affS3  cdZ1Ao5D  iKH9t6m9  mg4g9Eoi  oxeNN5uA  rzQKjmcB  w80nVzZO  zmrLJtwD

2CyEUmhf  5ntikrlo  8d6678sz  BpkwKiOq  FYfLvi5w  JLE4rtY5  MV2AJR5r  PkxFO6fj  Rrq6u3VG  W7K36eZ0  ZO3IvMwL  chvVzQdY  ih4q9ziU  mqsieQoa  oyrMYyZY  s3TrU3bC  w8E8Jd9J  zoSxd2Nl

2MgqiK3F  5ymaOO07  9LMKbufv  C0PnAa7J  FcWqkSIP  JLuwL5UE  MXItXLsj  PoAr7OrB  STlIDlxJ  WYlISi4n  ZQ7ftng7  cmhkISVH  jQXi84ic  myF2mI2w  p0qmvEGQ  sGOAdKy2  wHR2ydKC  zp4ssY0Q

2R1dcXMM  6GzNwIbL  9YFDyvy5  C3l9qdYz  FhDH2g8j  JVT3ckAg  MYdMdURn  PtRzswzh  Scml7yYd  WaA6y2oF  ZZzeAnnA  cvnPhBaQ  jnOnhjk8  n1PE7llz  p3lVedu9  sKOkwRCd  wvNy3kRU

2SLEujSI  6dZQoo4O  9rtRtn1R  CChBmQFs  FkO80Me6  JhHZxLSp  MavUz60O  QBtXtwy6  Sn9XVrp6  WjUfazgU  aDI9kNj8  d0OYmJbG  kDlGNWXG  n6yqXRv8  pREkecwB  svPh5fI5  xZDQnhCn

2cdcb2de  6mT8PiGl  9wXkj9wB  CDg6fdfa  FlEOSTL0  JrbVOugk  Md3PHwRz  QCHOeksH  TWbymLFA  WnH4XGQ0  aUzSODcp  d0rJvLyw  kQMlzWUP  nSepPhk6  pV3BIyJh  t4IiokLf  y2XXKk9C

2eijwTPh  760ZV0rr  9wzwojIO  CTTDdMGJ  GEtA0Z9a  KAS20Z1p  MvDDPtoW  QOHEW95s  TXecNl9L  WnOWGw9n  agmwERM5  d1usLAwO  kTDaKoIe  nTEqj1Ol  pVFybOWo  tenQzijC  y8THzTYH

3FOFUCD5  7KoII9M8  A2SZHgJV  CXVq5spu  GFWqPjn6  KCoDTFB7  NAwNCfiS  QTetbcxE  Tx4sSuiN  WwobUdQA  b5TZpaRr  dxJZggkO  kvSPifOB  nU797aVT  qAUGa8Jx  tkv0UoX3  yOmzIQym
```

There are a lot of files to check so I need to write a command that can loop each file and check it with the decrypt shell script given by the server. The following bash script loops through each file and runs the decryption command for it
  
```
ctf-player@pico-chall$ for i in $(find files); do ./decrypt.sh $i; done
```

find files is a command that will list out all of the files in the directory. For more information, here is the documentation of the [find command](https://man7.org/linux/man-pages/man1/find.1.html). In the for loop, i will represent a file and that file is an argument for the decrypt shell executable.

After running the command above, I looked over the output and found the flag. The solution is  
  
`picoCTF{trust_but_verify_2cdcb2de}`
  
The file that contained this information is `files/2cdcb2de`