<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <el-container>
    <el-header>
      <el-row>
        <el-col :span="2">
          <RouterLink to="/">Home</RouterLink>
        </el-col>
        <el-col :span="2">
          <RouterLink to="/about">About</RouterLink>
        </el-col>
      </el-row>
    </el-header>
    <el-main>
      <RouterView />
    </el-main>
  </el-container>
</template>

<style scoped></style>
