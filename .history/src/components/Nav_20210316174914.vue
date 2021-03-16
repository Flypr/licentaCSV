<template>
    <div class="navigation">
        <ul class="nav-ul">
            <li class="nav-link"><router-link to="/">Home</router-link></li>
            <li class="nav-link"><router-link to="/register">Register</router-link></li>
            <li class="nav-link"><router-link to="/login">Login</router-link></li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'Nav'
}
</script>