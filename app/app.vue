<template>
  <div class="min-h-screen bg-slate-50 text-slate-900">
    <header class="border-b bg-white">
      <div class="mx-auto max-w-6xl px-6 py-4 flex items-center justify-between">
        <div>
          <p class="text-xs uppercase tracking-[0.2em] text-slate-500">Broadview Heating & Air MVP</p>
          <h1 class="text-xl font-semibold">Dispatch Control Center</h1>
        </div>
        <button class="rounded-lg px-4 py-2 text-white font-medium" style="background:#299CD3">Create Work Order</button>
      </div>
    </header>

    <main class="mx-auto max-w-6xl px-6 py-8 grid gap-6 md:grid-cols-3">
      <section class="md:col-span-2 space-y-4">
        <div class="rounded-xl bg-white border p-5">
          <h2 class="font-semibold">Live Service Windows</h2>
          <div class="mt-4 grid sm:grid-cols-2 gap-3">
            <div v-for="job in windows" :key="job.id" class="rounded-lg border p-3">
              <p class="font-medium">{{ job.customer }}</p>
              <p class="text-sm text-slate-600">{{ job.service }}</p>
              <p class="text-sm mt-1">Window: <span class="font-medium">{{ job.window }}</span></p>
              <p class="text-xs mt-2" :class="job.sla < 30 ? 'text-rose-600' : 'text-emerald-600'">SLA buffer: {{ job.sla }} min</p>
            </div>
          </div>
        </div>

        <div class="rounded-xl bg-white border p-5">
          <h2 class="font-semibold">Flat-Rate Estimate Queue</h2>
          <table class="w-full mt-3 text-sm">
            <thead class="text-slate-500 text-left">
              <tr><th class="py-2">Customer</th><th>Trade</th><th>Total</th><th>Status</th></tr>
            </thead>
            <tbody>
              <tr v-for="q in quotes" :key="q.customer" class="border-t">
                <td class="py-2">{{ q.customer }}</td><td>{{ q.trade }}</td><td>{{ q.total }}</td><td>{{ q.status }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>

      <aside class="space-y-4">
        <div class="rounded-xl bg-white border p-5">
          <h2 class="font-semibold">Tech Capacity</h2>
          <ul class="mt-3 space-y-2 text-sm">
            <li v-for="t in techs" :key="t.name" class="flex justify-between">
              <span>{{ t.name }}</span><span class="text-slate-600">{{ t.load }}</span>
            </li>
          </ul>
        </div>
        <div class="rounded-xl border p-5 text-white" style="background:#E82C71">
          <h3 class="font-semibold">Today KPI</h3>
          <p class="mt-2 text-sm">92% jobs dispatched within promised 2-hour window.</p>
        </div>
      </aside>
    </main>
  </div>
</template>

<script setup lang="ts">
const windows = [
  { id: 1, customer: 'M. Reyes', service: 'Furnace tune-up', window: '10:00–12:00', sla: 42 },
  { id: 2, customer: 'J. Nelson', service: 'Water heater swap', window: '11:00–1:00', sla: 25 },
  { id: 3, customer: 'P. Adams', service: 'A/C diagnostics', window: '1:00–3:00', sla: 61 },
  { id: 4, customer: 'K. Moore', service: 'Panel inspection', window: '2:00–4:00', sla: 18 }
]

const quotes = [
  { customer: 'Riverview Bakery', trade: 'HVAC', total: '$4,860', status: 'Awaiting approval' },
  { customer: 'Bennett Home', trade: 'Plumbing', total: '$1,240', status: 'Sent to CRM' },
  { customer: 'Cedar Dental', trade: 'Electrical', total: '$2,980', status: 'Follow-up due' }
]

const techs = [
  { name: 'A. Boyd', load: '5 jobs' },
  { name: 'L. Patel', load: '4 jobs' },
  { name: 'D. Clark', load: '6 jobs' },
  { name: 'S. Kim', load: '3 jobs' }
]
</script>
