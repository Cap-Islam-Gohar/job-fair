<template>
    <div class="flow-root overflow-hidden">
        <div class="overflow-y-hidden overflow-x-auto">
            <table class="min-w-full colips min-h-full divide-y divide-gray-300">
                <thead>
                    <tr>
                        <slot name="thead"></slot>
                    </tr>
                </thead>
                <tbody class="divide-y divide-gray-300"> 
                    <slot name="tbody"></slot>                   
                </tbody>
                <tfoot class="text-center">
                    <slot name="tfoot"></slot>
                </tfoot>
            </table>
        </div>
    </div>
</template>
