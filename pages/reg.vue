<template>
  <div>
    <div class="col-md-4 m-auto p-3 mt-5">
      <div class="card ">
        <div class="card-header bg-success"><h3 class=" fw-bold fs-5 text-light">SIGNUP</h3></div>
        <div class="card-body">
          <form @submit.prevent="reg">
        <div class="mb-3">
          <label for="exampleInputEmail1" class="form-label">Email</label>
          <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" v-model="email">
        </div>
        <div class="mb-3">
          <label for="exampleInputPassword1" class="form-label" >Password</label>
          <input type="password" class="form-control" id="exampleInputPassword1"  v-model="password">
        </div>
        <button type="submit" class="btn btn-primary text-light me-3">Submit</button>
        <button type="submit" class="btn btn-warning">
          <NuxtLink to="/login">Kembali</NuxtLink>
        </button>
      </form>
        </div>
      </div>
    </div>
  </div>  
</template>

<script setup>
definePageMeta({
  middleware: 'auth'
})
  const supabase = useSupabaseAuthClient()
  const email = ref()
  const password = ref()

async function reg() {
  const { error } = await supabase
    .auth
    .signUp({
      email: email.value,
      password: password.value
    })

  navigateTo('/login')
}
</script>
