<template>
    <div class="w-full border rounded-xl px-4 sm:px-6 lg:px-8 py-6 sm:py-8 lg:py-10 mt-10 sm:mt-20">
        <div class="sm:flex sm:items-center space-y-2">
            <div class="sm:flex-auto">
                <slot name="card-title"></slot>
            </div>
            <div class="sm:ml-12 min-w-60 sm:flex-none">
                <slot name="card-option"></slot>
            </div>
        </div>
        <slot name="card-body"></slot>
    </div>
</template>