<template>
    <div id="chatbox" :class="{ 'altezza0': iconizza }">
        <div id="chatmenu" class="grid grid-cols-4 grid-rows-1 text-center">

            <i class="pi pi-users"></i>
            <i class="pi pi-inbox"></i>


            <DropdownLink :href="route('logout')" method="post" as="button">
                Log Out
            </DropdownLink>

            <i class="pi pi-circle-fill color-yellow-500" @click="iconizzachat"></i>
        </div>
        <hr />
        <div v-if="!iconizza">
     
            <Friendslist v-if="props.currentUser" :open="friendslist" v-show="friendslist"
                :currentUser="props.currentUser" @user="userselected">
            </Friendslist>

            <ChatMessage v-if="friend && chatmessages" v-show="chatmessages" @chiudichat="chiudichat" :friend="friend"
                :currentUser="currentUser" id="chatview"></ChatMessage>
        </div>

    </div>
</template>

<script setup>
import Friendslist from "./Friendslist.vue";
import ChatMessage from "./ChatMessage.vue"
import DropdownLink from '@/Components/DropdownLink.vue';
import { ref } from "vue";

const props = defineProps({
    currentUser: {
        type: Object,
        required: true,
        default: null
    },
});

const friendslist = ref(true);
const chatmessages = ref(false);
const friend = ref(null);
const iconizza = ref(false);


function userselected(val) {
    friend.value = val;
    friendslist.value = false;
    chatmessages.value = true;
    // getmessages(val.id);
}

function chiudichat(val) {
    friendslist.value = true;
    chatmessages.value = false;

}

function iconizzachat() {
    iconizza.value = !iconizza.value
}



</script>
<style scoped>
#chatbox {
    height: 500px;
    width: 400px;
    border: 1px solid rgb(221, 221, 221);

}

#chatmenu {
    height: 50px;

}

#chatmenu i {
    align-self: center;
}



.altezza0 {
    height: 50px !important;
}
</style>
