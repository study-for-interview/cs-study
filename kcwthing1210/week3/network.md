# ๐ OSI 7๊ณ์ธต
# ๐ ํ์ ๋ฐฐ๊ฒฝ

- ์ด๊ธฐ ์ฌ๋ฌ ์ ๋ณด ํต์  ์์ฒด ์ฅ๋น๋ค์ ์์ ์ ์์ฒด ์ฅ๋น๋ค๋ผ๋ฆฌ๋ง ์ฐ๊ฒฐ์ด ๋์ด ํธํ์ฑ์ด ์์์
- ๋ชจ๋  ์์คํ๋ค์ ์ํธ ์ฐ๊ฒฐ์ ์์ด ๋ฌธ์ ์๋๋ก ํ์ค์ ์ ํ๊ฒ์ด OSI 7๊ณ์ธต
- ํ์ค(ํธํ์ฑ)๊ณผ ํ์ต๋๊ตฌ์ ์๋ฏธ๋ก ์ ์

# ๐์๋ ์๋ฆฌ
1. OSI 7๊ณ์ธต์ ์์ฉ, ํํ, ์ธ์, ์ ์ก, ๋คํธ์ํฌ, ๋ฐ์ดํฐ๋งํฌ, ๋ฌผ๋ฆฌ๊ณ์ธต์ผ๋ก ๋๋จ.
1. ์ ์ก ์ 7๊ณ์ธต์์ 1๊ณ์ธต์ผ๋ก ๊ฐ๊ฐ์ ์ธต๋ง๋ค ์ธ์ํ  ์ ์์ด์ผ ํ๋ ํค๋๋ฅผ ๋ถ์(์บก์ํ)
3. ์์  ์ 1๊ณ์ธต์์ 7๊ณ์ธต์ผ๋ก ํค๋๋ฅผ ๋ผ์ด๋(๋์บก์ํ)
4. ์ถ๋ฐ์ง์์ ๋ฐ์ดํฐ๊ฐ ์ ์ก๋  ๋ ํค๋๊ฐ ์ถ๊ฐ๋๋๋ฐ 2๊ณ์ธต์์๋ง ์ค๋ฅ์ ์ด๋ฅผ ์ํด ๊ผฌ๋ฆฌ๋ถ๋ถ์ ์ถ๊ฐ๋
5. ๋ฌผ๋ฆฌ๊ณ์ธต์์ 1, 0 ์ ์ ํธ๊ฐ ๋์ด ์ ์ก๋งค์ฒด (๋์ถ์ผ์ด๋ธ, ๊ด์ฌ์  ๋ฑ)์ ํตํด ์ ์ก

# ๐OSI 7๊ณ์ธต
![](https://images.velog.io/images/kcwthing1210/post/bd56fdc6-b6e1-44fe-8bb8-3584c4ac89a7/image.png)

## โ ๋ฌผ๋ฆฌ๊ณ์ธต(Physical Layer)
- 7๊ณ์ธต ์ค ์ตํ์ ๊ณ์ธต.
- ์ฃผ๋ก ์ ๊ธฐ์ , ๊ธฐ๊ณ์ , ๊ธฐ๋ฅ์ ์ธ ํน์ฑ์ ์ด์ฉํด ๋ฐ์ดํฐ๋ฅผ ์ ์ก.
- ๋ฐ์ดํฐ๋ 0๊ณผ 1์ ๋นํธ์ด, ์ฆ On, Off์ ์ ๊ธฐ์  ์ ํธ ์ํ๋ก ์ด๋ฃจ์ด์ ธ ํด๋น ๊ณ์ธต์ ๋จ์ง ๋ฐ์ดํฐ๋ฅผ ์ ๋ฌ.
- ๋จ์ง ๋ฐ์ดํฐ ์ ๋ฌ์ ์ญํ ์ ํ  ๋ฟ์ด๋ผ ์๊ณ ๋ฆฌ์ฆ, ์ค๋ฅ์ ์ด ๊ธฐ๋ฅ์ด ์์
- ์ฅ๋น๋ก๋ ์ผ์ด๋ธ, ๋ฆฌํผํฐ, ํ๋ธ๊ฐ ์์
## โ ๋ฐ์ดํฐ๋งํฌ ๊ณ์ธต(Data-Link Layer)
- ๋ฌผ๋ฆฌ์ ์ธ ์ฐ๊ฒฐ์ ํตํ์ฌ ์ธ์ ํ ๋ ์ฅ์น ๊ฐ์ ์ ๋ขฐ์ฑ ์๋ ์ ๋ณด ์ ์ก์ ๋ด๋น(Point-To-Point ์ ์ก)
- ์์ ํ ์ ๋ณด์ ์ ๋ฌ์ด๋ผ๋ ๊ฒ์ ์ค๋ฅ๋ ์ฌ์ ์กํ๋ ๊ธฐ๋ฅ์ด ์กด์ฌ
- MAC ์ฃผ์๋ฅผ ํตํด์ ํต์ 
- ๋ฐ์ดํฐ ๋งํฌ ๊ณ์ธต์์ ๋ฐ์ดํฐ ๋จ์๋ ํ๋ ์(Frame)
- ์ฅ๋น๋ก๋ ๋ธ๋ฆฌ์ง, ์ค์์น๊ฐ ์์
## โ ๋คํธ์ํฌ ๊ณ์ธต(Network Layer)
- ์ค๊ณ ๋ธ๋๋ฅผ ํตํ์ฌ ์ ์กํ๋ ๊ฒฝ์ฐ ์ด๋ป๊ฒ ์ค๊ณํ  ๊ฒ์ธ๊ฐ๋ฅผ ๊ท์ 
- ๋ผ์ฐํ ๊ธฐ๋ฅ์ ๋งก๊ณ  ์๋ ๊ณ์ธต์ผ๋ก ๋ชฉ์ ์ง๊น์ง ๊ฐ์ฅ ์์ ํ๊ณ  ๋น ๋ฅด๊ฒ ๋ฐ์ดํฐ๋ฅผ ๋ณด๋ด๋ ๊ธฐ๋ฅ์ ๊ฐ์ง๊ณ  ์์(์ต์ ์ ๊ฒฝ๋ก๋ฅผ ์ค์ ๊ฐ๋ฅ)
- ์ปดํจํฐ์๊ฒ ๋ฐ์ดํฐ๋ฅผ ์ ์กํ ์ง ์ฃผ์๋ฅผ ๊ฐ๊ณ  ์์ด์ ํต์ ๊ฐ๋ฅ(=์ฐ๋ฆฌ๊ฐ ์์ฃผ ๋ฃ๋ IP ์ฃผ์๊ฐ ๋ฐ๋ก ๋คํธ์ํฌ ๊ณ์ธต ํค๋์ ์ํจ)
- ๋คํธ์ํฌ ๊ณ์ธต์์ ๋ฐ์ดํฐ ๋จ์๋ ํจํท(Packet)
- ์ฅ๋น๋ก๋ ๋ผ์ฐํฐ, L3 ์ค์์น๊ฐ ์์
## โ ์ ์ก ๊ณ์ธต(Transport Layer)
- ์ข๋จ ๊ฐ ์ ๋ขฐ์ฑ ์๊ณ  ์ ํํ ๋ฐ์ดํฐ ์ ์ก์ ๋ด๋น
- ์ก์ ์์ ์์ ์ ๊ฐ์ ์ ๋ขฐ์ฑ์๊ณ  ํจ์จ์ ์ธ ๋ฐ์ดํฐ๋ฅผ ์ ์กํ๊ธฐ ์ํ์ฌ ์ค๋ฅ๊ฒ์ถ ๋ฐ ๋ณต๊ตฌ, ํ๋ฆ์ ์ด์ ์ค๋ณต๊ฒ์ฌ ๋ฑ์ ์ํ
- ๋ฐ์ดํฐ ์ ์ก์ ์ํด์ Port ๋ฒํธ๋ฅผ ์ฌ์ฉํจ.(๋ํ์ ์ธ ํ๋กํ ์ฝ๋ก TCP์ UDP๊ฐ ์์)
- ์ ์ก ๊ณ์ธต์์ ๋ฐ์ดํฐ ๋จ์๋ ์ธ๊ทธ๋จผํธ(Segment)
## โ ์ธ์ ๊ณ์ธต(Session Layer)
- ํต์  ์ฅ์น ๊ฐ ์ํธ์์ฉ ๋ฐ ๋๊ธฐํ๋ฅผ ์ ๊ณต
- ์ฐ๊ฒฐ ์ธ์์์ ๋ฐ์ดํฐ ๊ตํ๊ณผ ์๋ฌ ๋ฐ์ ์์ ๋ณต๊ตฌ๋ฅผ ๊ด๋ฆฌ
## โ ํํ ๊ณ์ธต(Presentation Layer)
- ๋ฐ์ดํฐ๋ฅผ ์ด๋ป๊ฒ ํํํ ์ง ์ ํ๋ ์ญํ ์ ํ๋ ๊ณ์ธต
- ํํ ๊ณ์ธต์ ์ธ๊ฐ์ง์ ๊ธฐ๋ฅ์ ๊ฐ๊ณ  ์์ต๋๋ค.
    -  ์ก์ ์์์ ์จ ๋ฐ์ดํฐ๋ฅผ ํด์ํ๊ธฐ ์ํ ์์ฉ๊ณ์ธต ๋ฐ์ดํฐ ๋ถํธํ, ๋ณํ
    - ์์ ์์์ ๋ฐ์ดํฐ์ ์์ถ์ ํ์ ์๋ ๋ฐฉ์์ผ๋ก ๋ ๋ฐ์ดํฐ ์์ถ
    - ๋ฐ์ดํฐ์ ์ํธํ์ ๋ณตํธํ
      (MIME ์ธ์ฝ๋ฉ์ด๋ ์ํธํ ๋ฑ์ ๋์์ด ํํ๊ณ์ธต์์ ์ด๋ฃจ์ด์ง. EBCDIC๋ก ์ธ์ฝ๋ฉ๋ ํ์ผ์ ASCII ๋ก ์ธ์ฝ๋ฉ๋ ํ์ผ๋ก ๋ฐ๊ฟ์ฃผ๋ ๊ฒ์ด ํ๊ฐ์ง ์์)
## โ ์์ฉ ๊ณ์ธต(Application Layer)
- ์ฌ์ฉ์์ ๊ฐ์ฅ ๋ฐ์ ํ ๊ณ์ธต์ผ๋ก ์ธํฐํ์ด์ค ์ญํ 
- ์์ฉ ํ๋ก์ธ์ค ๊ฐ์ ์ ๋ณด ๊ตํ์ ๋ด๋น
- ex) ์ ์๋ฉ์ผ, ์ธํฐ๋ท, ๋์์ ํ๋ ์ด์ด ๋ฑ

# ๐งฉ Reference
- https://velog.io/@cgotjh/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-OSI-7-%EA%B3%84%EC%B8%B5-OSI-7-LAYER-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-%EA%B0%81-%EA%B3%84%EC%B8%B5-%EC%84%A4%EB%AA%85
- https://mommoo.tistory.com/107