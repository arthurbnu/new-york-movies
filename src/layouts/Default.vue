<template>
  <!-- <div :data-theme="theme"> -->
    <div >
    <!-- <div class="navbar fixed bg-slate-900 z-40 shadow-sm">
      <div class="navbar-start">
        <a class="btn btn-ghost text-lg md:text-xl text-teal-600">
          <span class="bold">
          <i class="las la-film "></i>
            <i class="las la-map-marker "></i>
        </span>
          New York movies ...</a>
      </div>
      <div class="navbar-center hidden lg:flex">
      </div>
    </div> -->
    <slot />
    <footer class="footer footer-center p-10 bg-base-50">
      <div>
        <span class="text-2xl md:text-3xl font-bold">New York movies ...</span>
      </div>
      <div>
        <div class="grid grid-flow-col gap-4">
        
        </div>
      </div>
    </footer>
  </div>
</template>

