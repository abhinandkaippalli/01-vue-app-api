<template>
    <div class="container">
        <div class="row">
            <div class="col-md-6">
                <div class="card">
                    <div class="card-body">
                        <div v-if="isLoggedIn">
                            <p class="h3 fw-bold text-success">Welcome User</p>
                            <p class="fst-italic">
                                Many novice writers tend to make a sharp distinction between content and style, thinking
                                that a paper can be strong in one and weak in the other, but focusing on organization shows
                                how content and
                                style converge in deliberative academic writing.
                            </p>
                        </div>
                        <div v-if="!isLoggedIn">
                            <p class="h3 fw-bold text-danger">Thank You!!</p>
                            <p class="fst-italic">
                                Many novice writers tend to make a sharp distinction between content and style, thinking
                                that a paper can be strong in one and weak in the other.
                            </p>
                        </div>
                        <div>
                            <button v-if="!isLoggedIn" class="btn btn-success btn-sm m-1" @click="login()">Login</button>
                            <button v-if="isLoggedIn" class="btn btn-danger btn-sm m-1" @click="logout()">Log Out</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'AuthUser',
    data: function () {
        return {
            isLoggedIn: false
        }
    },
    methods: {
        login: function () {
            this.isLoggedIn = true
        },
        logout: function () {
            this.isLoggedIn = false
        }
    }
}
</script>

<style></style>