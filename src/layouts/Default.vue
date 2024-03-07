<template>
  <!-- <div :data-theme="theme"> -->
    <div >
    <div class="navbar fixed bg-slate-900 z-40 shadow-sm">
      <div class="navbar-start">
        <a class="btn btn-ghost text-xl text-teal-600">

          <span class="bold">
          <i class="las la-film "></i>  <i class="las la-map-marker "></i>
        </span>
          New York movies ...</a>
      </div>
      <div class="navbar-center hidden lg:flex">
        <!-- TODO: You can add menu here -->
      </div>
    </div>
    <slot />
    <footer class="footer footer-center p-10 bg-base-50">
      <div>
        <h1 class="text-2xl md:text-3xl font-bold">New York movies ...</h1>
      </div>
      <div>
        <div class="grid grid-flow-col gap-4">
        
        </div>
      </div>
    </footer>
  </div>
</template>

