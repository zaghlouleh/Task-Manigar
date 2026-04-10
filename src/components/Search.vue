<template>
  <div id="app">
    <div class="search-wrapper" style="position:relative">
      <input type="Search" v-model="search" class=" bg-gray-200" >
       <font-awesome-icon icon="search" class=" text-gray-500" style="left:9px;top:10px;position:absolute "/>
    </div>
    <div class="wrapper">
      <div class="card" v-for="post in filteredList" :key="post">
        <a v-bind:href="post.link" target="_blank">
          <img v-bind:src="post.img" />
          <small>posted by: {{ post.author }}</small>
          {{ post.title }}
        </a>
      </div>
    </div>
  </div>
</template>
<script>
export default{
  
}
</script>
<style  scoped>

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.search-wrapper {
  position: relative;
}
label {
  position: absolute;
  font-size: 12px;
  color: rgba(0, 0, 0, 0.5);
  top: 8px;
  left: 12px;
  z-index: -1;
  transition: 0.15s all ease-in-out;
}
input {
  padding: 4px 12px;
  color: rgba(0, 0, 0, 0.7);
  border: 2px solid rgb(218, 217, 217);
  transition: 0.15s all ease-in-out;
  border-radius: 10px;
}
input:focus {
  outline: none;
  transform: scale(1.05);
}
label:focus {
  font-size: 10px;
  transform: translateY(-24px) translateX(-12px);
}

label::-webkit-input-placeholder {
  font-size: 12px;
  color: rgba(0, 0, 0, 0.5);
  font-weight: 100;
}

.wrapper {
  display: flex;
  max-width: 444px;
  flex-wrap: wrap;
  padding-top: 12px;
}

.card {
  box-shadow: rgba(0, 0, 0, 0.117647) 0px 1px 6px,
    rgba(0, 0, 0, 0.117647) 0px 1px 4px;
  max-width: 124px;
  margin: 12px;
  transition: 0.15s all ease-in-out;
}
.card :hover {
  transform: scale(1.1);
}
a {
  text-decoration: none;
  padding: 12px;
  color: #03a9f4;
  font-size: 24px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
img {
  height: 100px;
}
small {
  font-size: 10px;
  padding: 4px;
 
}

</style>