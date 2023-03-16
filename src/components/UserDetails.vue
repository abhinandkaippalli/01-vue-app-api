<template>
    <div class="container mt-3">
        <div v-if="loading">
            <SpinnerVue />
        </div>
        <div class="row" v-if="'!loading && bject.keys(user).length > 0'">
            <div class="col">
                <pre>{{ user }}</pre>
            </div>
        </div>
    </div>
    <div class="row">
        <div class="col">
            <router-link class="btn btn-success ms-3" to="/users">Back</router-link>
        </div>
    </div>
</template> 

<script>
import { UserService } from '@/services/UserService';
import SpinnerVue from './SpinnerVue.vue';

export default {
    name: "UserDetails",
    data: function () {
        return {
            loading: false,
            user: [],
            errorMessage: null
        };
    },
    created: async function () {
        let userId = this.$route.params.userId;
        try {
            this.loading = true;
            let res = await UserService.getUser(userId);
            this.loading = false;
            this.user = res.data;
            console.log(res.data);
        }
        catch (error) {
            this.loading = false;
            this.errorMessage = error;
            console.log(error);
        }
    },
    components: { SpinnerVue }
}
</script>

<style>

</style>