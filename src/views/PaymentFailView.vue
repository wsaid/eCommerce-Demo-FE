<template>
  <main class="grid min-h-full place-items-center bg-white px-6 py-24 sm:py-32 lg:px-8">
    <div class="text-center">
      <p class="text-base font-semibold text-indigo-600">
        <svg class="inline" width="70px" height="70px" viewBox="0 0 512 512" version="1.1" xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink">
          <title>error-filled</title>
          <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
            <g id="add" fill="#AA0300" transform="translate(42.666667, 42.666667)">
              <path
                d="M213.333333,3.55271368e-14 C331.136,3.55271368e-14 426.666667,95.5306667 426.666667,213.333333 C426.666667,331.136 331.136,426.666667 213.333333,426.666667 C95.5306667,426.666667 3.55271368e-14,331.136 3.55271368e-14,213.333333 C3.55271368e-14,95.5306667 95.5306667,3.55271368e-14 213.333333,3.55271368e-14 Z M262.250667,134.250667 L213.333333,183.168 L164.416,134.250667 L134.250667,164.416 L183.168,213.333333 L134.250667,262.250667 L164.416,292.416 L213.333333,243.498667 L262.250667,292.416 L292.416,262.250667 L243.498667,213.333333 L292.416,164.416 L262.250667,134.250667 Z"
                id="Combined-Shape">

              </path>
            </g>
          </g>
        </svg>
      </p>
      <h1 class="mt-4 text-3xl font-bold tracking-tight text-red-400 sm:text-4xl">Payment Failed!</h1>

      <p class="mt-6 text-base leading-7 text-gray-600">Insufficient funds.</p>
      <div class="mt-10 flex items-center justify-center gap-x-6">
        <RouterLink to="/" class="rounded-md bg-indigo-600 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
          Go back home
        </RouterLink>
        <RouterLink to="/cart" class="text-sm font-semibold text-gray-900">
          Go back to shopping cart
        </RouterLink>
      </div>
  </div>
</main></template>