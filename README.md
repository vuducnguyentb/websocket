Ví dụ về websocket
Tạo Khi mà ta chạy router: /test-event sẽ bắn 1 cái event vào chanel sang bên client
Ở đây bắn data là user 
Khi bắn thì ở phía client chạy laravel-echo-server start
✔  Running at localhost on port 6001
✔  Channels are ready.
✔  Listening for http events...
✔  Listening for redis events...

Server ready!

[2022-05-21T04:23:12.049Z] - Qi8UB1qgNaJ-t51FAAAA joined channel: chat
[2022-05-21T04:23:12.071Z] - Qi8UB1qgNaJ-t51FAAAA joined channel: chat
Channel: chat
Event: App\Events\NewMessage



**Step 1: create-project laravel**
**Step 2:**

require laravel/ui (composer require laravel/ui)
php artisan ui vue --auth
**Step 3:**

install Laravel-echo + socket.io (npm install --save-dev laravel-echo socket.io-client@2.4.0)
install Laravel-echo-server (https://github.com/tlaverdure/laravel-echo-server)
**Step 4: Cấu hình laravel-echo-server**
import Echo from 'laravel-echo';

window.io = require('socket.io-client');

window.Echo = new Echo({
broadcaster: 'socket.io',
host: window.location.hostname + ':6001'
});

**Step 5: Make Event (php artisan make:event NewMessage)**
+ Note: có 3 kiểu channel: public, private, presence

public function broadcastOn() // define channel
{
return new Channel('chat');
}

public function broadcastWith() { //return data channel
return ['user' => $this->user];
}

**Step 6: config database**

**Step 7: cấu hình env**
Mặc định BROADCAST_DRIVER=log. Khi broadcast sẽ ghi log dữ liệu lại
install predis (composer require predis/predis).
Sau đó cấu hình lại môi trường

BROADCAST_DRIVER=redis
REDIS_CLIENT=predis
REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379
REDIS_PREFIX=""

**Step 8: receiving data**
window.Echo.channel('chat')
.listen('NewMessage', (data) => {
console.log('data', data)
});
