<template>

    <div>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <div class="collapse navbar-collapse">
                <div class="navbar-nav" v-if="loggedUser">
                    <h5>Daslllhboard</h5>
                    <a href="javascript:void(0)" @click="logout()" class="nav-item nav-link ml-3">Logout</a>
                </div>
                <div v-else>
                    <router-link to="/login">Login</router-link>
                    <router-link to="/register">Register</router-link>
                </div>
            </div>
        </nav>
        <h1>Dashboard Dashboard</h1>
        <button  @click="logout()">logout</button>
        <h4>The logged in user details Here</h4><br>
        <p> {{user.name}}</p>
        <p> {{user.email}}</p>
    </div>
</template>
<script>
    // export default {
    //     data () {
    //         return {
    //             user: this.auth.user
    //         }
    //     },
    //     created() {
    //         // console.log(this.auth.user);
    //     }


            import Auth from '../Auth';
    export default {
        data() {
            return {
                 user: this.auth.user,
                loggedUser: this.auth.user
            };
        },
        mounted() {
            console.log(this.auth.user);
        },
        methods: {
            logout() {
                this.axios.post('http://127.0.0.1:8000/api/logout')
                .then(({data}) => {
                    Auth.logout(); //reset local storage
                    this.$router.push('/login');
                })
                .catch((error) => {
                    console.log(error);
                });
            }
        }
    }
    // }
</script>