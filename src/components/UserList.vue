<template>
    <div class="container mt-3">
        <div class="row">
            <div class="col">
                <p class="h3 fw-bold text-success">User List</p>
                <p class="fst-italic">
                    style converge in deliberative academic writing. Your professors will view even the most elegant prose
                    as
                    rambling and tedious if there isn’t a careful, coherent argument to give the text meaning. Paragraphs
                    are the
                    “stuff ” of academic writing and, thus, worth our attention here
                </p>
            </div>

            <div v-if="loading">
                <SpinnerVue />
            </div>

            <div v-if="errorMessage">
                <p class="fw-bold text-danger">{{ errorMessage }}</p>
            </div>

            <div class="row" v-if="!loading && users.length > 0">
                <div class="col">
                    <table class="table table-hover text-center table-striped">
                        <thead class="bg-success text-white">
                            <tr>
                                <th>Sno</th>
                                <th>Name</th>
                                <th>Email</th>
                                <th>Company</th>
                                <th>Website</th>
                                <th>Location</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="user in users" :key="user.id">
                                <td>{{ user.id }}</td>
                                <td>
                                    <RouterLink :to="'/users/' + user.id" class="text-decoration-none fw-bold text-success" >{{ user.name }}</RouterLink>
                                </td>
                                <td>{{ user.email }}</td>
                                <td>{{ user.company.name }}</td>
                                <td>{{ user.website }}</td>
                                <td>{{ user.address.city }}</td>
                            </tr>
                        </tbody>
                    </table>  
                </div>
            </div>
        </div>
    </div>
</template>

<script>

import { UserService } from '@/services/UserService'
import SpinnerVue from './SpinnerVue.vue'

export default {
    name: "UserList",
    data: function () {
        return {
            loading: false,
            users: [],
            errorMessage: null
        };
    },
    created: async function () {
        try {
            this.loading = true;
            let res = await UserService.getAllUsers();
            this.loading = false;
            this.users = res.data;
            console.log(res.data);
        }
        catch (error) {
            console.log(error);
            this.loading = false;
            this.errorMessage = error;
        }
    },
    components: { SpinnerVue }
}
</script>

<style></style>