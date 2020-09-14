<template>
<div id="app">
    <div class="min-h-screen">
        <div class="px-3 pt-8 pb-4 font-montserrat font-semibold lg:max-w-screen-lg lg:mx-auto lg:pt-16">
            <header>
                <h1 class="text-2xl leading-7 text-black-1 lg:text-4xl">Checkout</h1>
            </header>
            <main>
                <div class="lg:flex lg:flex-row-reverse">
                    <div class="mt-5 lg:mt-12">
                        <div class="rounded-12px bg-gray-6 px-6">
                            <div>
                                <div v-for="item in cart" :key="item.id" class="flex pt-6">
                                    <div>
                                        <img class="h-32 w-32 rounded-13px" :src="require(`@/assets/images/${item.photo}`)" :alt="item.name">
                                    </div>
                                    <div class="px-5">
                                        <p class="text-xs leading-4 lg:text-base">{{ item.name }}</p>
                                        <p class="text-sm leading-4 text-orange-400 pt-2 lg:text-base">${{ item.currentPrice }} <span class="text-10px text-black-1 line-through mx-2 lg:text-xs">${{ item.originalPrice }}</span></p>
                                        <div class="flex mt-6 rounded-12px border border-black-2">
                                            <div class="flex items-center justify-center py-2 px-2">
                                                <button @click="item.items--" class="bg-gray-5 rounded-sm w-5 h-5 flex items-center justify-center focus:outline-none" type="button">
                                                    <p class="text-gray-3">-</p>
                                                </button>
                                            </div>
                                            <div class="flex-1 text-center justify-center">
                                                <div class="py-2">
                                                    <p>{{item.items}}</p>
                                                </div>
                                            </div>
                                            <div class="flex items-center justify-center py-2 px-2">
                                                <button @click="item.items++" class="bg-gray-5 rounded-sm w-5 h-5 flex items-center justify-center focus:outline-none" type="button">
                                                    <p class="text-gray-3">+</p>
                                                </button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="pb-4 mt-16">
                                <div class="flex items-center justify-between border-t border-gray-4 py-2">
                                    <p class="text-sm leading-4 text-gray-1">Shipping</p>
                                    <p class="text-sm leading-4 text-gray-1">$19</p>
                                </div>
                                <div class="flex items-center justify-between border-t border-gray-4 py-2">
                                    <p class="text-sm leading-4 text-gray-1">Total</p>
                                    <p class="text-sm leading-4 text-gray-1">{{fetchTotal}}</p>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="lg:flex-1 lg:mr-24 lg:px-4">
                        <div class="mt-8 lg:mt-12">
                            <h2 class="text-sm leading-4 text-gray-1 lg:text-lg">Contact information</h2>
                            <div class="mt-3 lg:mt-6">
                                <label class="block text-10px text-gray-2 leading-3 lg:text-xs" for="email">E-mail</label>
                                <div class="flex items-center mt-1 p-3 border border-gray-3 rounded-12px">
                                    <div class="inline-block">
                                        <svg class="h-4 w-4 text-gray-3 fill-current" viewBox="0 0 24 24">
                                            <path fill="currentColor" d="M20 8l-8 5-8-5V6l8 5 8-5m0-2H4c-1.11 0-2 .89-2 2v12a2 2 0 002 2h16a2 2 0 002-2V6a2 2 0 00-2-2z" />
                                        </svg>
                                    </div>
                                    <div class="inline-block text-xs leading-4 ml-3">
                                        <input class="bg-transparent focus:outline-none" type="email" v-model.trim="formData.email" placeholder="Enter your email..." id="email">
                                    </div>
                                </div>
                            </div>
                            <div class="mt-4">
                                <label class="block text-10px text-gray-2 leading-3 lg:text-xs" for="phone">Phone</label>
                                <div class="flex items-center mt-1 p-3 border border-gray-3 rounded-12px">
                                    <div class="inline-block">
                                        <svg class="h-4 w-4 text-gray-3 fill-current" viewBox="0 0 24 24">
                                            <path fill="currentColor" d="M6.62 10.79c1.44 2.83 3.76 5.15 6.59 6.59l2.2-2.2c.28-.28.67-.36 1.02-.25 1.12.37 2.32.57 3.57.57a1 1 0 011 1V20a1 1 0 01-1 1A17 17 0 013 4a1 1 0 011-1h3.5a1 1 0 011 1c0 1.25.2 2.45.57 3.57.11.35.03.74-.25 1.02l-2.2 2.2z" />
                                        </svg>
                                    </div>
                                    <div class="inline-block text-xs leading-4 ml-3">
                                        <input class="bg-transparent focus:outline-none" type="text" v-model.number="formData.phone" placeholder="Enter your phone..." id="phone">
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="mt-10">
                            <h2 class="text-sm leading-4 text-gray-1 lg:text-lg">Shipping address</h2>
                            <div class="mt-3 lg:mt-6">
                                <label class="block text-10px text-gray-2 leading-3 lg:text-xs" for="name">Full name</label>
                                <div class="flex items-center mt-1 p-3 border border-gray-3 rounded-12px">
                                    <div class="inline-block">
                                        <svg class="h-4 w-4 text-gray-3 fill-current" viewBox="0 0 24 24">
                                            <path fill="currentColor" d="M20 8l-8 5-8-5V6l8 5 8-5m0-2H4c-1.11 0-2 .89-2 2v12a2 2 0 002 2h16a2 2 0 002-2V6a2 2 0 00-2-2z" />
                                        </svg>
                                    </div>
                                    <div class="inline-block text-xs leading-4 ml-3">
                                        <input class="bg-transparent focus:outline-none" type="text" v-model.trim="formData.name" id="name">
                                    </div>
                                </div>
                            </div>
                            <div class="mt-4">
                                <label class="block text-10px text-gray-2 leading-3 lg:text-xs" for="address">Address</label>
                                <div class="flex items-center mt-1 p-3 border border-gray-3 rounded-12px">
                                    <div class="inline-block">
                                        <svg class="h-4 w-4 text-gray-3 fill-current" viewBox="0 0 24 24">
                                            <path fill="currentColor" d="M10,20V14H14V20H19V12H22L12,3L2,12H5V20H10Z" />
                                        </svg>
                                    </div>
                                    <div class="inline-block text-xs leading-4 ml-3">
                                        <input class="bg-transparent focus:outline-none" type="text" placeholder="Your address.." v-model.trim="formData.address" id="address">
                                    </div>
                                </div>
                            </div>
                            <div class="mt-3">
                                <label class="block text-10px text-gray-2 leading-3 lg:text-xs" for="city">City</label>
                                <div class="flex items-center mt-1 p-3 border border-gray-3 rounded-12px">
                                    <div class="inline-block">
                                        <svg class="h-4 w-4 text-gray-3 fill-current" viewBox="0 0 24 24">
                                            <path fill="currentColor" d="M19,15H17V13H19M19,19H17V17H19M13,7H11V5H13M13,11H11V9H13M13,15H11V13H13M13,19H11V17H13M7,11H5V9H7M7,15H5V13H7M7,19H5V17H7M15,11V5L12,2L9,5V7H3V21H21V11H15Z" />
                                        </svg>
                                    </div>
                                    <div class="inline-block text-xs leading-4 ml-3">
                                        <input class="bg-transparent focus:outline-none" type="text" placeholder="Your city.." v-model.trim="formData.city" id="city">
                                    </div>
                                </div>
                            </div>
                            <div class="flex mt-3 justify-between">
                                <div class="w-48">
                                    <label class="block text-10px text-gray-2 leading-3 lg:text-xs" for="country">Country</label>
                                    <div class="flex items-center mt-1 p-3 border border-gray-3 rounded-12px">
                                        <div class="inline-block">
                                            <svg class="h-4 w-4 text-gray-3 fill-current" viewBox="0 0 24 24">
                                                <path fill="currentColor" d="M17.9,17.39C17.64,16.59 16.89,16 16,16H15V13A1,1 0 0,0 14,12H8V10H10A1,1 0 0,0 11,9V7H13A2,2 0 0,0 15,5V4.59C17.93,5.77 20,8.64 20,12C20,14.08 19.2,15.97 17.9,17.39M11,19.93C7.05,19.44 4,16.08 4,12C4,11.38 4.08,10.78 4.21,10.21L9,15V16A2,2 0 0,0 11,18M12,2A10,10 0 0,0 2,12A10,10 0 0,0 12,22A10,10 0 0,0 22,12A10,10 0 0,0 12,2Z" />
                                            </svg>
                                        </div>
                                        <div class="inline-block text-xs leading-4 ml-3 w-full">
                                            <select name="country" id="country" class="focus:outline-none w-full" v-model="formData.country">
                                                <option class="text-gray-2" value="">Your country...</option>
                                                <option v-for="country in country" :key="country" :value="country">{{country}}</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>
                                <div class="w-48 ml-4">
                                    <label class="block text-10px text-gray-2 leading-3 lg:text-xs" for="postalCode">Postal code</label>
                                    <div class="flex items-center mt-1 p-3 border border-gray-3 rounded-12px">
                                        <div class="inline-block">
                                            <svg class="h-4 w-4 text-gray-3 fill-current" viewBox="0 0 24 24">
                                                <path fill="currentColor" d="M17,14H19V17H22V19H19V22H17V19H14V17H17V14M10,2H14A2,2 0 0,1 16,4V6H20A2,2 0 0,1 22,8V13.53C20.94,12.58 19.54,12 18,12A6,6 0 0,0 12,18C12,19.09 12.29,20.12 12.8,21H4C2.89,21 2,20.1 2,19V8C2,6.89 2.89,6 4,6H8V4C8,2.89 8.89,2 10,2M14,6V4H10V6H14Z" />
                                            </svg>
                                        </div>
                                        <div class="inline-block text-xs leading-4 ml-3 w-full">
                                            <input class="bg-transparent focus:outline-none w-full" type="text" placeholder="Your postal code.." v-model.trim="formData.postalCode" id="postalCode">
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="mt-4 flex items-center">
                                <input id="remember" type="checkbox" v-model="formData.remember">
                                <label for="remember" class="inline-block text-10px text-gray-2 ml-2 lg:text-xs">Save this information for next time</label>
                            </div>
                        </div>
                        <div class="mt-5 text-right">
                            <div class="inline-block py-4 px-10 rounded-12px bg-orange-400 hover:bg-orange-500">
                                <button class="text-base leading-5 text-white focus:outline-none">Continue</button>
                            </div>
                        </div>
                    </div>
                </div>
            </main>
            <footer class="mt-16">
                <p class="text-xs leading-4 text-footer text-center">Nisarg Patel @ DevChallenges.io</p>
            </footer>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'App',
    components: {},
    data() {
        return {
            country: ['Canada', 'India', 'Mexico'],
            formData: {
                email: '',
                phone: '',
                name: 'Rodney Cotton',
                address: '',
                city: '',
                country: '',
                postalCode: '',
                remember: false,
            },
            cart: [{
                    id: 1,
                    name: 'Vintage Backbag',
                    photo: 'photo1.png',
                    currentPrice: 54.99,
                    originalPrice: 94.99,
                    items: 1,
                },
                {
                    id: 2,
                    name: 'Levi Shoes',
                    photo: 'photo2.png',
                    currentPrice: 74.99,
                    originalPrice: 124.99,
                    items: 1,
                }
            ],
            shipping: 19,
        }
    },
    computed: {
        fetchTotal() {
            let total = 0;
            this.cart.forEach(function (item) {
                let itemTotal = (item.currentPrice * item.items);
                total += itemTotal;
            });
            return (total + this.shipping).toFixed(2);
        }
    }
}
</script>

<style lang="scss">
#app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
</style>
