<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">User Info</div>

                    <div class="card-body">
                       <p>User Name : {{user.name}}</p>
                       <p>User Email : {{user.email}}</p>
                       <p></p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
          return{
              user: {}
          }  
        },
        mounted() {
            console.log('Component mounted.');
            let _this = this;
            window.Echo.channel('chat')
                .listen('NewMessage', (data) => {
                    console.log('Chạy vào kênh r');
                console.log('data', data);
                _this.user = data.user;
                        });
        }
    }
</script>
