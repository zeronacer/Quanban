<template>
    <div class="list-group-item" :key="cardName">
        <div class="row">
            <div class="col">
                <span>{{ cardName }}</span>
            </div>
            <div class="col">
                <b-button type="button" class="close align-top" aria-label="Close" @click="$emit('delete-card', cardName)">
                    <span class="align-text-top" aria-hidden="true">
                        <svg width="0.7em" height="0.7em" viewBox="0 0 16 16" class="bi bi-trash-fill" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                            <path fill-rule="evenodd" d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5a.5.5 0 0 0-1 0v7a.5.5 0 0 0 1 0v-7z"/>
                        </svg>
                    </span>
                </b-button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    cardName: String
  }
}
</script>