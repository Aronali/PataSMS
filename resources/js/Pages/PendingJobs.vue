<script setup>
import { Head } from '@inertiajs/vue3';
import AppLayout from "@/Layouts/AppLayout.vue";
import {defineOptions} from "vue";
import TableHead from "@/Components/TableHead.vue";
import TableHeadItem from "@/Components/TableHeadItem.vue";
import TableBody from "@/Components/TableBody.vue";
import TableBodyItem from "@/Components/TableBodyItem.vue";
import TableData from "@/Components/TableData.vue";
import Pagination from "@/Components/Pagination.vue";
import Table from "@/Components/Table.vue";
import IconButton from "@/Components/IconButton.vue";

defineOptions({
    layout: AppLayout,
})

const props = defineProps({
    jobs: {
        type: Object,
    }
})

const retryJob = (id) => {
    console.log(id)
}
</script>

<template>

    <Head title="Pending Jobs"/>

    <div>
        <h2 class="py-6 text-2xl font-semibold text-gray-700 dark:text-gray-200">
            Pending Jobs
        </h2>
    </div>

    <Table >
        <template #thead>
            <TableHead>
                <TableHeadItem field="name"/>
                <TableHeadItem field="progress"/>
                <TableHeadItem field="status"/>
                <TableHeadItem field="finished"/>
            </TableHead>
        </template>
        <template #tbody>
            <TableBody v-if="jobs.data.length > 0">
                <TableBodyItem v-for="job in jobs.data">

                       <TableData >
                           {{ job.name ?? '-' }}
                       </TableData>
                       <TableData >
                           {{ `${job.batch[0].progress}%` ?? '-' }}
                       </TableData>
                       <TableData >
                        <span v-if="!job.batch[0].failed && job.batch[0].finishedAt" class="bg-green-100 text-green-800 text-xs font-medium mr-2 px-2.5 py-0.5 rounded-full">
                           completed
                        </span>
                           <span v-else-if="job.batch[0].failed && job.batch[0].finishedAt" class="bg-red-100 text-red-800 text-xs font-medium mr-2 px-2.5 py-0.5 rounded-full">
                             failed
                        </span>
                           <span v-else class="bg-gray-100 text-gray-800 text-xs font-medium mr-2 px-2.5 py-0.5 rounded-full">
                           pending
                        </span>
                       </TableData>
                       <TableData>
                           {{ job.batch[0].finishedAt ?? '-' }}
                       </TableData>

                </TableBodyItem>
            </TableBody>

            <TableBody v-else>
                <TableBodyItem>
                    <TableData colspan="6" class="text-center text-gray-500">
                        There is nothing to show here
                    </TableData>
                </TableBodyItem>
            </TableBody>

        </template>
        <template #pagination>
            <Pagination v-if="jobs.links" :to="jobs.to" :from="jobs.from" :total="jobs.total" :links="jobs.links" />
        </template>
    </Table>
</template>
