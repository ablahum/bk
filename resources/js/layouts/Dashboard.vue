<template>
    <div class="flex h-screen bg-gray-200">
        <div
            :class="sidebarOpen ? 'block' : 'hidden'"
            @click="sidebarOpen = false"
            class="fixed inset-0 z-20 transition-opacity bg-black opacity-50 lg:hidden"
        ></div>

        <div
            :class="
                sidebarOpen
                    ? 'translate-x-0 ease-out'
                    : '-translate-x-full ease-in'
            "
            class="fixed inset-y-0 left-0 z-30 w-64 overflow-y-auto transition duration-300 transform bg-gray-900 lg:translate-x-0 lg:static lg:inset-0"
        >
            <div class="flex items-center justify-center my-8">
                <div class="flex items-center">
                    <svg
                        class="w-12 h-12"
                        viewBox="0 0 512 512"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            d="M364.61 390.213C304.625 450.196 207.37 450.196 147.386 390.213C117.394 360.22 102.398 320.911 102.398 281.6C102.398 242.291 117.394 202.981 147.386 172.989C147.386 230.4 153.6 281.6 230.4 307.2C230.4 256 256 102.4 294.4 76.7999C320 128 334.618 142.997 364.608 172.989C394.601 202.981 409.597 242.291 409.597 281.6C409.597 320.911 394.601 360.22 364.61 390.213Z"
                            fill="#4C51BF"
                            stroke="#4C51BF"
                            stroke-width="2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        ></path>
                        <path
                            d="M201.694 387.105C231.686 417.098 280.312 417.098 310.305 387.105C325.301 372.109 332.8 352.456 332.8 332.8C332.8 313.144 325.301 293.491 310.305 278.495C295.309 263.498 288 256 275.2 230.4C256 243.2 243.201 320 243.201 345.6C201.694 345.6 179.2 332.8 179.2 332.8C179.2 352.456 186.698 372.109 201.694 387.105Z"
                            fill="white"
                        ></path>
                    </svg>

                    <span class="text-2xl font-semibold text-white capitalize"
                        >bumi kahuripan</span
                    >
                </div>
            </div>

            <nav>
                <div
                    :class="[
                        'flex items-center px-6 py-2 mt-4 text-gray-500 hover:bg-gray-700 hover:bg-opacity-25 hover:text-gray-100',
                        $route.path === '/orders'
                            ? 'text-gray-100 bg-gray-700 bg-opacity-25'
                            : '',
                    ]"
                >
                    <svg
                        class="w-6 h-6"
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M11 3.055A9.001 9.001 0 1020.945 13H11V3.055z"
                        ></path>
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M20.488 9H15V3.512A9.025 9.025 0 0120.488 9z"
                        ></path>
                    </svg>

                    <span class="mx-3 capitalize">
                        <RouterLink to="/orders" class="m-0"
                            >pesanan</RouterLink
                        >
                    </span>
                </div>

                <div
                    :class="[
                        'flex items-center px-6 py-2 mt-4 text-gray-500 hover:bg-gray-700 hover:bg-opacity-25 hover:text-gray-100',
                        $route.path === '/rooms'
                            ? 'text-gray-100 bg-gray-700 bg-opacity-25'
                            : '',
                    ]"
                    v-if="user && user.role.name === 'admin'"
                >
                    <svg
                        class="w-6 h-6"
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                    >
                        <path
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            stroke-width="2"
                            d="M17 14v6m-3-3h6M6 10h2a2 2 0 002-2V6a2 2 0 00-2-2H6a2 2 0 00-2 2v2a2 2 0 002 2zm10 0h2a2 2 0 002-2V6a2 2 0 00-2-2h-2a2 2 0 00-2 2v2a2 2 0 002 2zM6 20h2a2 2 0 002-2v-2a2 2 0 00-2-2H6a2 2 0 00-2 2v2a2 2 0 002 2z"
                        ></path>
                    </svg>

                    <span class="mx-3 capitalize">
                        <RouterLink to="/rooms" class="m-0">kamar</RouterLink>
                    </span>
                </div>
            </nav>
        </div>

        <div class="flex flex-col flex-1 overflow-hidden">
            <header
                class="flex items-center justify-between px-6 py-4 bg-white border-b-4 border-indigo-600"
            >
                <button
                    @click="sidebarOpen = true"
                    class="text-gray-500 focus:outline-none lg:hidden"
                >
                    <svg
                        class="w-6 h-6"
                        viewBox="0 0 24 24"
                        fill="none"
                        xmlns="http://www.w3.org/2000/svg"
                    >
                        <path
                            d="M4 6H20M4 12H20M4 18H11"
                            stroke="currentColor"
                            stroke-width="2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                        ></path>
                    </svg>
                </button>

                <div
                    class="flex items-center lg:gap-0 gap-4 lg:justify-between justify-end w-full"
                >
                    <p class="capitalize">
                        selamat datang,
                        <span class="font-semibold"> {{ user.name }}! </span>
                    </p>

                    <button
                        class="outline outline-red-500 uppercase px-3 py-1 rounded-lg text-red-500 font-semibold"
                        @click="logout"
                    >
                        keluar
                    </button>
                </div>
            </header>

            <RouterView :current-path="currentPath" />
        </div>
    </div>
</template>

<script>
import { getMe, logout } from "../apis/auth";

export default {
    data() {
        return {
            sidebarOpen: false,
            user: "",
        };
    },
    mounted() {
        this.getProfile();
    },
    computed: {
        currentPath() {
            return this.$route.path;
        },
    },
    methods: {
        async getProfile() {
            const res = await getMe();

            this.user = res.data.user;
        },
        async logout() {
            try {
                const res = await logout();

                if (res.status === 200) {
                    alert("Logout berhasil.");
                    localStorage.removeItem("auth-token");
                    this.$router.push("/login");
                }
            } catch (err) {
                console.error(err.response.data);
            }
        },
    },
};
</script>
