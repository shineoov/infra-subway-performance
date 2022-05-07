<p align="center">
    <img width="200px;" src="https://raw.githubusercontent.com/woowacourse/atdd-subway-admin-frontend/master/images/main_logo.png"/>
</p>
<p align="center">
  <img alt="npm" src="https://img.shields.io/badge/npm-%3E%3D%205.5.0-blue">
  <img alt="node" src="https://img.shields.io/badge/node-%3E%3D%209.3.0-blue">
  <a href="https://edu.nextstep.camp/c/R89PYi5H" alt="nextstep atdd">
    <img alt="Website" src="https://img.shields.io/website?url=https%3A%2F%2Fedu.nextstep.camp%2Fc%2FR89PYi5H">
  </a>
  <img alt="GitHub" src="https://img.shields.io/github/license/next-step/atdd-subway-service">
</p>

<br>

# 인프라공방 샘플 서비스 - 지하철 노선도

<br>

## 🚀 Getting Started

### Install
#### npm 설치
```
cd frontend
npm install
```
> `frontend` 디렉토리에서 수행해야 합니다.

### Usage
#### webpack server 구동
```
npm run dev
```
#### application 구동
```
./gradlew clean build
```
<br>

## 미션

* 미션 진행 후에 아래 질문의 답을 작성하여 PR을 보내주세요.


### 1단계 - 화면 응답 개선하기
1. 성능 개선 결과를 공유해주세요 (Smoke, Load, Stress 테스트 결과)

#### Smoke Test

**데이터를 조회하는데 여러 데이터를 참조하는 페이지 - ( 경로검색 )**  

```
$ k6 run --out influxdb=http://localhost:8086/myk6db smoke_path.js

          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: smoke_path.js
     output: InfluxDBv1 (http://localhost:8086)

  scenarios: (100.00%) 1 scenario, 1 max VUs, 15m30s max duration (incl. graceful stop):
           * default: 1 looping VUs for 15m0s (gracefulStop: 30s)


running (15m00.5s), 0/1 VUs, 818 complete and 0 interrupted iterations
default ↓ [======================================] 1 VUs  15m0s

     ✓ http status code 200
     ✓ stations is json path exist

     checks.........................: 100.00% ✓ 1636     ✗ 0
     data_received..................: 4.3 MB  4.7 kB/s
     data_sent......................: 97 kB   107 B/s
     http_req_blocked...............: avg=22.97µs min=257ns   med=312ns   max=23.47ms  p(90)=482ns    p(95)=564ns
     http_req_connecting............: avg=459ns   min=0s      med=0s      max=436.24µs p(90)=0s       p(95)=0s
   ✗ http_req_duration..............: avg=49.84ms min=1.23ms  med=5ms     max=171.16ms p(90)=105.48ms p(95)=115.37ms
       { expected_response:true }...: avg=49.84ms min=1.23ms  med=5ms     max=171.16ms p(90)=105.48ms p(95)=115.37ms
     http_req_failed................: 0.00%   ✓ 0        ✗ 1636
     http_req_receiving.............: avg=91.9µs  min=23.12µs med=59.65µs max=4.73ms   p(90)=155.17µs p(95)=282.52µs
     http_req_sending...............: avg=67.74µs min=29.7µs  med=63.58µs max=3.93ms   p(90)=79.94µs  p(95)=89.02µs
     http_req_tls_handshaking.......: avg=9.23µs  min=0s      med=0s      max=12.7ms   p(90)=0s       p(95)=0s
     http_req_waiting...............: avg=49.68ms min=1.17ms  med=4.9ms   max=166.35ms p(90)=105.28ms p(95)=115.23ms
     http_reqs......................: 1636    1.816792/s
     iteration_duration.............: avg=1.1s    min=1s      med=1.09s   max=1.19s    p(90)=1.11s    p(95)=1.12s
     iterations.....................: 818     0.908396/s
     vus............................: 1       min=1      max=1
     vus_max........................: 1       min=1      max=1
   ✓ waitingTimeOnCachedData........: avg=1.79ms  min=1.17ms  med=1.53ms  max=12.3ms   p(90)=2.33ms   p(95)=3.18ms
```

**접속 빈도가 높은 페이지 ( 메인 페이지 )**

```
$ k6 run --out influxdb=http://localhost:8086/myk6db smoke_main.js

          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: smoke_main.js
     output: InfluxDBv1 (http://localhost:8086)

  scenarios: (100.00%) 1 scenario, 1 max VUs, 15m30s max duration (incl. graceful stop):
           * default: 1 looping VUs for 15m0s (gracefulStop: 30s)


running (15m00.9s), 0/1 VUs, 886 complete and 0 interrupted iterations
default ✓ [======================================] 1 VUs  15m0s

     ✓ logged in successfully
     ✓ retrieved member

     checks.....................: 100.00% ✓ 1772     ✗ 0
     data_received..............: 490 kB  543 B/s
     data_sent..................: 155 kB  172 B/s
     http_req_blocked...........: avg=22.45µs min=234ns   med=302ns   max=23.42ms  p(90)=473ns   p(95)=527ns
     http_req_connecting........: avg=322ns   min=0s      med=0s      max=307.53µs p(90)=0s      p(95)=0s
   ✓ http_req_duration..........: avg=7.87ms  min=4.55ms  med=9.07ms  max=18.44ms  p(90)=9.87ms  p(95)=10.25ms
     http_req_failed............: 100.00% ✓ 1772     ✗ 0
     http_req_receiving.........: avg=49.66µs min=21.62µs med=47.78µs max=268.14µs p(90)=64.63µs p(95)=70.9µs
     http_req_sending...........: avg=60.89µs min=25.63µs med=60.94µs max=462.51µs p(90)=81.56µs p(95)=91.66µs
     http_req_tls_handshaking...: avg=8.04µs  min=0s      med=0s      max=11.98ms  p(90)=0s      p(95)=0s
     http_req_waiting...........: avg=7.76ms  min=4.48ms  med=8.94ms  max=18.31ms  p(90)=9.74ms  p(95)=10.12ms
     http_reqs..................: 1772    1.966959/s
     iteration_duration.........: avg=1.01s   min=1.01s   med=1.01s   max=1.04s    p(90)=1.01s   p(95)=1.01s
     iterations.................: 886     0.983479/s
     vus........................: 1       min=1      max=1
     vus_max....................: 1       min=1      max=1

```

**데이터를 갱신 하는 페이지 ( 지하철역 등록 )**  

```
$ k6 run --out influxdb=http://localhost:8086/myk6db smoke_station.js

          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: smoke_station.js
     output: InfluxDBv1 (http://localhost:8086)

  scenarios: (100.00%) 1 scenario, 1 max VUs, 15m30s max duration (incl. graceful stop):
           * default: 1 looping VUs for 15m0s (gracefulStop: 30s)



running (15m00.8s), 0/1 VUs, 885 complete and 0 interrupted iterations
default ↓ [======================================] 1 VUs  15m0s

   ✓ Content Created................: 100.00% ✓ 885      ✗ 0
     data_received..................: 284 kB  316 B/s
     data_sent......................: 100 kB  111 B/s
     http_req_blocked...............: avg=31.34µs min=258ns   med=297ns   max=27.42ms  p(90)=383ns   p(95)=423ns
     http_req_connecting............: avg=298ns   min=0s      med=0s      max=264.22µs p(90)=0s      p(95)=0s
   ✓ http_req_duration..............: avg=17ms    min=12.49ms med=15.14ms max=699.07ms p(90)=18.81ms p(95)=21.1ms
       { expected_response:true }...: avg=17ms    min=12.49ms med=15.14ms max=699.07ms p(90)=18.81ms p(95)=21.1ms
   ✓ http_req_failed................: 0.00%   ✓ 0        ✗ 885
     http_req_receiving.............: avg=59.02µs min=36.58µs med=57.8µs  max=254.61µs p(90)=69.92µs p(95)=75.08µs
     http_req_sending...............: avg=75.71µs min=50.52µs med=71.14µs max=236.59µs p(90)=90.56µs p(95)=100.34µs
     http_req_tls_handshaking.......: avg=14.72µs min=0s      med=0s      max=13.03ms  p(90)=0s      p(95)=0s
     http_req_waiting...............: avg=16.87ms min=12.36ms med=15.01ms max=698.92ms p(90)=18.67ms p(95)=20.97ms
     http_reqs......................: 885     0.982457/s
     iteration_duration.............: avg=1.01s   min=1.01s   med=1.01s   max=1.69s    p(90)=1.01s   p(95)=1.02s
     iterations.....................: 885     0.982457/s
     vus............................: 1       min=1      max=1
     vus_max........................: 1       min=1      max=1
```

#### Load Test

**데이터를 조회하는데 여러 데이터를 참조하는 페이지 - ( 경로검색 )**  
```
    $ k6 run --out influxdb=http://localhost:8086/myk6db load_path.js
    
              /\      |‾‾| /‾‾/   /‾‾/
         /\  /  \     |  |/  /   /  /
        /  \/    \    |     (   /   ‾‾\
       /          \   |  |\  \ |  (‾)  |
      / __________ \  |__| \__\ \_____/ .io
    
      execution: local
         script: load_path.js
         output: InfluxDBv1 (http://localhost:8086)
    
      scenarios: (100.00%) 1 scenario, 110 max VUs, 15m30s max duration (incl. graceful stop):
               * default: Up to 110 looping VUs for 15m0s over 5 stages (gracefulRampDown: 30s, gracefulStop: 30s)
    
    
    
    
    running (15m04.2s), 000/110 VUs, 19282 complete and 0 interrupted iterations
    default ↓ [======================================] 110/110 VUs  15m0s
    
         ✓ http status code 200
         ✓ stations is json path exist
    
         checks.........................: 100.00% ✓ 38564     ✗ 0
         data_received..................: 99 MB   109 kB/s
         data_sent......................: 2.3 MB  2.6 kB/s
         http_req_blocked...............: avg=14.45µs  min=145ns    med=341ns   max=48.59ms p(90)=584ns    p(95)=668ns
         http_req_connecting............: avg=1.37µs   min=0s       med=0s      max=5.01ms  p(90)=0s       p(95)=0s
       ✗ http_req_duration..............: avg=793.72ms min=991.94µs med=3.58ms  max=6.49s   p(90)=3.31s    p(95)=3.44s
           { expected_response:true }...: avg=793.72ms min=991.94µs med=3.58ms  max=6.49s   p(90)=3.31s    p(95)=3.44s
         http_req_failed................: 0.00%   ✓ 0         ✗ 38564
         http_req_receiving.............: avg=106.1µs  min=13.93µs  med=59.13µs max=19.5ms  p(90)=137.43µs p(95)=296.05µs
         http_req_sending...............: avg=71.09µs  min=19.56µs  med=62.06µs max=15.77ms p(90)=92.95µs  p(95)=109.94µs
         http_req_tls_handshaking.......: avg=10.93µs  min=0s       med=0s      max=30.13ms p(90)=0s       p(95)=0s
         http_req_waiting...............: avg=793.54ms min=0s       med=3.38ms  max=6.49s   p(90)=3.31s    p(95)=3.44s
         http_reqs......................: 38564   42.649771/s
         iteration_duration.............: avg=2.58s    min=1s       med=2.09s   max=7.49s   p(90)=4.44s    p(95)=4.51s
         iterations.....................: 19282   21.324886/s
         vus............................: 10      min=1       max=110
         vus_max........................: 110     min=110     max=110
         waitingTimeOnCachedData........: avg=2.09ms   min=0s       med=1.7ms   max=45.93ms p(90)=3.16ms   p(95)=4.41ms
```    

**접속 빈도가 높은 페이지 ( 메인 페이지 )**  

```
$ k6 run --out influxdb=http://localhost:8086/myk6db load_main.js

          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: load_main.js
     output: InfluxDBv1 (http://localhost:8086)

  scenarios: (100.00%) 1 scenario, 110 max VUs, 15m30s max duration (incl. graceful stop):
           * default: Up to 110 looping VUs for 15m0s over 5 stages (gracefulRampDown: 30s, gracefulStop: 30s)



running (15m01.0s), 000/110 VUs, 48602 complete and 0 interrupted iterations
default ✓ [======================================] 000/110 VUs  15m0s

     ✓ logged in successfully
     ✓ retrieved member

     checks.....................: 100.00% ✓ 97204      ✗ 0
     data_received..............: 27 MB   30 kB/s
     data_sent..................: 8.5 MB  9.4 kB/s
     http_req_blocked...........: avg=6.78µs  min=161ns   med=334ns   max=25.5ms   p(90)=495ns   p(95)=558ns
     http_req_connecting........: avg=690ns   min=0s      med=0s      max=17.06ms  p(90)=0s      p(95)=0s
   ✓ http_req_duration..........: avg=11.18ms min=4.57ms  med=9.45ms  max=203.56ms p(90)=18.36ms p(95)=23.55ms
     http_req_failed............: 100.00% ✓ 97204      ✗ 0
     http_req_receiving.........: avg=46.75µs min=11.9µs  med=34.41µs max=44.22ms  p(90)=59.11µs p(95)=73.8µs
     http_req_sending...........: avg=51.82µs min=17.65µs med=43.55µs max=18.85ms  p(90)=71.55µs p(95)=83.96µs
     http_req_tls_handshaking...: avg=5.04µs  min=0s      med=0s      max=18.56ms  p(90)=0s      p(95)=0s
     http_req_waiting...........: avg=11.08ms min=1.43ms  med=9.34ms  max=203.44ms p(90)=18.24ms p(95)=23.42ms
     http_reqs..................: 97204   107.881292/s
     iteration_duration.........: avg=1.02s   min=1.01s   med=1.02s   max=1.23s    p(90)=1.03s   p(95)=1.04s
     iterations.................: 48602   53.940646/s
     vus........................: 4       min=1        max=110
     vus_max....................: 110     min=110      max=110
```

**데이터를 갱신 하는 페이지 ( 지하철역 등록 )**  

```
$ k6 run --out influxdb=http://localhost:8086/myk6db load_station.js

          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: load_station.js
     output: InfluxDBv1 (http://localhost:8086)

  scenarios: (100.00%) 1 scenario, 110 max VUs, 15m30s max duration (incl. graceful stop):
           * default: Up to 110 looping VUs for 15m0s over 5 stages (gracefulRampDown: 30s, gracefulStop: 30s)

running (15m01.0s), 000/110 VUs, 49166 complete and 0 interrupted iterations
default ✓ [======================================] 000/110 VUs  15m0s

   ✓ Content Created................: 100.00% ✓ 49166     ✗ 0
     data_received..................: 16 MB   18 kB/s
     data_sent......................: 5.8 MB  6.4 kB/s
     http_req_blocked...............: avg=9.39µs  min=152ns   med=295ns   max=27.98ms p(90)=442ns   p(95)=552ns
     http_req_connecting............: avg=1.44µs  min=0s      med=0s      max=13.23ms p(90)=0s      p(95)=0s
   ✓ http_req_duration..............: avg=10.82ms min=6.63ms  med=10.26ms max=47.75ms p(90)=13.43ms p(95)=15.12ms
       { expected_response:true }...: avg=10.82ms min=6.63ms  med=10.26ms max=47.75ms p(90)=13.43ms p(95)=15.12ms
   ✓ http_req_failed................: 0.00%   ✓ 0         ✗ 49166
     http_req_receiving.............: avg=45.96µs min=11.94µs med=34.2µs  max=15.02ms p(90)=65.33µs p(95)=82.2µs
     http_req_sending...............: avg=63.27µs min=19.27µs med=53.38µs max=12.35ms p(90)=98.18µs p(95)=121.95µs
     http_req_tls_handshaking.......: avg=6.3µs   min=0s      med=0s      max=12.92ms p(90)=0s      p(95)=0s
     http_req_waiting...............: avg=10.71ms min=6.55ms  med=10.15ms max=47.65ms p(90)=13.3ms  p(95)=15.01ms
     http_reqs......................: 49166   54.567879/s
     iteration_duration.............: avg=1.01s   min=1s      med=1.01s   max=1.06s   p(90)=1.01s   p(95)=1.01s
     iterations.....................: 49166   54.567879/s
     vus............................: 3       min=1       max=110
     vus_max........................: 110     min=110     max=110

```


#### Stress Test

**데이터를 조회하는데 여러 데이터를 참조하는 페이지 - ( 경로검색 )**  

```
$ k6 run --out influxdb=http://localhost:8086/myk6db stress_path.js

default ✓ [======================================] 330/330 VUs  15m0s

     ✗ http status code 200
      ↳  9% — ✓ 7835 / ✗ 72654
     ✗ stations is json path exist
      ↳  9% — ✓ 7835 / ✗ 72652

     checks.........................: 9.73%  ✓ 15670     ✗ 145306
     data_received..................: 118 MB 116 kB/s
     data_sent......................: 32 MB  32 kB/s
     http_req_blocked...............: avg=2.62ms   min=0s              med=0s       max=1.19s p(90)=312ns    p(95)=547ns
     http_req_connecting............: avg=50.66ms  min=0s              med=18.69ms  max=9m32s p(90)=61.73ms  p(95)=77.12ms
   ✗ http_req_duration..............: avg=2.02s    min=0s              med=0s       max=9m52s p(90)=263.42ms p(95)=3.5s
       { expected_response:true }...: avg=3.67s    min=1.01ms          med=838.43ms max=9m52s p(90)=11.78s   p(95)=12.42s
     http_req_failed................: 84.38% ✓ 74720     ✗ 13826
     http_req_receiving.............: avg=64.83ms  min=-495490187491ns med=0s       max=9m32s p(90)=57.34µs  p(95)=94.33µs
     http_req_sending...............: avg=6.51ms   min=0s              med=0s       max=1.22s p(90)=86.1µs   p(95)=140.15µs
     http_req_tls_handshaking.......: avg=8.38ms   min=0s              med=0s       max=1.53s p(90)=19.18ms  p(95)=71.61ms
     http_req_waiting...............: avg=1.95s    min=0s              med=0s       max=9m44s p(90)=139.88ms p(95)=3.5s
     http_reqs......................: 88546  87.240844/s
     iteration_duration.............: avg=1.23s    min=249.43µs        med=58.71ms  max=9m47s p(90)=937.12ms p(95)=5.17s
     iterations.....................: 80471  79.284868/s
     vus............................: 312    min=1       max=330
     vus_max........................: 330    min=330     max=330
     waitingTimeOnCachedData........: avg=151.04ms min=0s              med=1.67ms   max=2.81s p(90)=503.86ms p(95)=1.2s

```

**접속 빈도가 높은 페이지 ( 메인 페이지 )**

```
$ k6 run --out influxdb=http://localhost:8086/myk6db stress_main.js

          /\      |‾‾| /‾‾/   /‾‾/
     /\  /  \     |  |/  /   /  /
    /  \/    \    |     (   /   ‾‾\
   /          \   |  |\  \ |  (‾)  |
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: stress_main.js
     output: InfluxDBv1 (http://localhost:8086)

  scenarios: (100.00%) 1 scenario, 330 max VUs, 15m30s max duration (incl. graceful stop):
           * default: Up to 330 looping VUs for 15m0s over 8 stages (gracefulRampDown: 30s, gracefulStop: 30s)


running (15m00.8s), 000/330 VUs, 111796 complete and 0 interrupted iterations
default ↓ [======================================] 001/330 VUs  15m0s

     ✓ logged in successfully
     ✓ retrieved member

     checks.....................: 100.00% ✓ 223592     ✗ 0
     data_received..............: 62 MB   69 kB/s
     data_sent..................: 20 MB   22 kB/s
     http_req_blocked...........: avg=6.92µs  min=152ns    med=272ns   max=25.16ms  p(90)=388ns   p(95)=434ns
     http_req_connecting........: avg=747ns   min=0s       med=0s      max=16ms     p(90)=0s      p(95)=0s
   ✓ http_req_duration..........: avg=9.25ms  min=4.06ms   med=7.84ms  max=423.42ms p(90)=14.09ms p(95)=19.01ms
     http_req_failed............: 100.00% ✓ 223592     ✗ 0
     http_req_receiving.........: avg=53.01µs min=10.76µs  med=24.62µs max=31.64ms  p(90)=58.71µs p(95)=133.54µs
     http_req_sending...........: avg=47.98µs min=14.71µs  med=33.33µs max=26.81ms  p(90)=64.46µs p(95)=97.78µs
     http_req_tls_handshaking...: avg=5.41µs  min=0s       med=0s      max=13.91ms  p(90)=0s      p(95)=0s
     http_req_waiting...........: avg=9.15ms  min=253.96µs med=7.75ms  max=423.15ms p(90)=13.93ms p(95)=18.75ms
     http_reqs..................: 223592  248.226398/s
     iteration_duration.........: avg=1.01s   min=1.01s    med=1.01s   max=1.45s    p(90)=1.02s   p(95)=1.03s
     iterations.................: 111796  124.113199/s
     vus........................: 1       min=1        max=330
     vus_max....................: 330     min=330      max=330

```

**데이터를 갱신 하는 페이지 ( 지하철역 등록 )**

```
running (15m00.8s), 000/750 VUs, 153612 complete and 0 interrupted iterations
default ✓ [======================================] 000/750 VUs  15m0s

   ✗ Content Created................: 76.39% ✓ 117355     ✗ 36257
     data_received..................: 693 MB 769 kB/s
     data_sent......................: 109 MB 121 kB/s
     http_req_blocked...............: avg=174.3ms  min=0s    med=17.03ms  max=1.41s    p(90)=594.45ms p(95)=697.06ms
     http_req_connecting............: avg=2.53ms   min=0s    med=195.11µs max=189.18ms p(90)=4.14ms   p(95)=14.02ms
   ✗ http_req_duration..............: avg=569.55ms min=0s    med=106.03ms max=10.42s   p(90)=1.76s    p(95)=2.42s
       { expected_response:true }...: avg=698.58ms min=7.6ms med=281.95ms max=10.42s   p(90)=1.98s    p(95)=2.65s
   ✗ http_req_failed................: 23.60% ✓ 36257      ✗ 117355
     http_req_receiving.............: avg=518.45µs min=0s    med=36.96µs  max=171.02ms p(90)=304.51µs p(95)=1.18ms
     http_req_sending...............: avg=131.84ms min=0s    med=75.85µs  max=10.05s   p(90)=472.35ms p(95)=970.57ms
     http_req_tls_handshaking.......: avg=184.59ms min=0s    med=29.72ms  max=1.41s    p(90)=593.53ms p(95)=702.52ms
     http_req_waiting...............: avg=437.18ms min=0s    med=98.87ms  max=8.82s    p(90)=1.28s    p(95)=1.78s
     http_reqs......................: 153612 170.527678/s
     iteration_duration.............: avg=1.77s    min=1s    med=1.23s    max=11.91s   p(90)=3.2s     p(95)=3.88s
     iterations.....................: 153612 170.527678/s
     vus............................: 1      min=1        max=750
     vus_max........................: 750    min=750      max=750
```


2. 어떤 부분을 개선해보셨나요? 과정을 설명해주세요

`HTTP/2` 를 적용해보았고,  
`Gzip` 으로 콘텐츠 압축을 하여 전송되는 데이터양을 줄였습니다.    
정적인 파일 들을 `Cache` 설정하였습니다.  

위 설정은 정적인 파일 대상으로 효과가 있겠지만 API 테스트 에서는 `http_req_duration` 은 거의 줄지 않았고   
전송되는 미세하게 데이터양만 줄었습니다.  

애플리케이션 에서는  
경로검색 결과를 얻을 때 많을 리소스를 사용하고 변경이 많지 않아  
`Redis` 에 캐싱을 적용했습니다.  
경로 검색 로드 테스트는 http_req_duration max 가 572ms 에서  5.48ms 로 크게 효과를 보았습니다.   

`Nomad` 를 활용해 WAS 를 3대 추가로 띄워보긴 했는데
인스턴스 하나에 올려서 그런지 효과가 거의 없었습니다.



#### HTTP2 
```
server {  
    listen 443 ssl http2;
...
```

#### gzip
```
server {
  ...
  gzip on; 
  gzip_comp_level 9;
  gzip_vary on;
  gzip_types text/plain text/css application/json application/x-javascript application/javascript text/xml application/xml application/rss+xml text/javascript image/svg+xml application/vnd.ms-fontobject application/x-font-ttf font/opentype;
}

```
#### Static File Cache

```
http{
  ...
  proxy_cache_path /tmp/nginx keys_zone=CACHE:60m levels=1:2 inactive=24h max_size=1g;
  proxy_cache_key "$scheme$host$request_uri"; 
  ...
  server {
      ...
      location ~* \.(?:css|js|gif|png|jpg|jpeg)$ {
       add_header Cache-Control "public";
       add_header X-Proxy-Cache $upstream_cache_status;
       proxy_pass http://app;
       proxy_cache_valid 200 60m;
       proxy_cache CACHE;
       expires 1w;
       access_log off;
      ...
  }
}
  
```
#### Spring Data Cache
```java
    @Cacheable(value = "path", key = "{#source, #target}" )
    public PathResponse findPath(Long source, Long target) {
        List<Line> lines = lineService.findLines();
        Station sourceStation = stationService.findById(source);
        Station targetStation = stationService.findById(target);
        SubwayPath subwayPath = pathService.findPath(lines, sourceStation, targetStation);
        return PathResponseAssembler.assemble(subwayPath);
    }
```

#### Nomad Scale Out?
![실행결과](./images/nomad.png)


---

### 2단계 - 스케일 아웃

1. Launch Template 링크를 공유해주세요.

2. cpu 부하 실행 후 EC2 추가생성 결과를 공유해주세요. (Cloudwatch 캡쳐)

```sh
$ stress -c 2
```

3. 성능 개선 결과를 공유해주세요 (Smoke, Load, Stress 테스트 결과)

---

### 3단계 - 쿼리 최적화

1. 인덱스 설정을 추가하지 않고 아래 요구사항에 대해 1s 이하(M1의 경우 2s)로 반환하도록 쿼리를 작성하세요.

- 활동중인(Active) 부서의 현재 부서관리자 중 연봉 상위 5위안에 드는 사람들이 최근에 각 지역별로 언제 퇴실했는지 조회해보세요. (사원번호, 이름, 연봉, 직급명, 지역, 입출입구분, 입출입시간)

---

### 4단계 - 인덱스 설계

1. 인덱스 적용해보기 실습을 진행해본 과정을 공유해주세요

---

### 추가 미션

1. 페이징 쿼리를 적용한 API endpoint를 알려주세요
