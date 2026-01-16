```bash
CRM frontend KHÔNG tự query DB → nó luôn đi theo 3 tầng:
Doctype (schema)
   ↓
API chuẩn của Frappe (reportview / client / CRM api)
   ↓
frappe-ui (createResource / ListView / Modal)

- KHÔNG viết backend mới nếu chưa cần
- 90% CRUD dùng API có sẵn
```

# Tạo Doctype (bắt buộc)
**Ở đâu**
```bash
CRM > Developer > DocType
```
**Ex**
```bash
Simple Item
- title (Data, reqd)
- description (Small Text)
- quantity (Int)
- status (Select: Draft\nActive\nInactive)

- Check:
    + Is Submittable ❌
    + Is Tree ❌
    + Allow Rename ❌

XONG → DB có bảng
```

# Frontend structure (chuẩn crm)
frontend/src/pages/simple-item/
```bash
simple-item/
├─ SimpleItemList.vue        (page)
├─ SimpleItemListView.vue    (component | list + bulk actions)
├─ SimpleItemModal.vue       (component |create / edit)

- CRM luôn tách như vậy
    + Page = orchestration
    + ListView = table + bulk
    + Modal = form
```

# FETCH LIST (KHÔNG VIẾT BACKEND)
Ở file page (SimpleItemList.vue)
```bash
const items = createResource({
  url: 'frappe.desk.reportview.get',
  params: {
    doctype: 'Simple Item',
    fields: ['name', 'title', 'description', 'quantity', 'status'],
    order_by: 'modified desc',
    limit_page_length: 50,
  },
  auto: true,
})
```
Dữ liệu trả về
```bash
values = [
  ['ID1', 'Title 1', 'Desc', 2, 'Draft'],
  ...

CRM dùng cách này 100%
]

# MAP → ROWS (FORMAT CHO LISTVIEW)
const rows = computed(() =>
  items.data?.values.map((r) => ({
    name: r[0],
    title: { label: r[1] },
    description: { label: r[2] },
    quantity: { label: r[3] },
    status: { label: r[4] },
  })) || []
)


⚠️ BẮT BUỘC

mỗi cell = { label: value }

name phải tồn tại

HIỂN THỊ LIST (GIỐNG CRM)

📍 SimpleItemListView.vue

<ListView
  :rows="rows"
  :columns="columns"
  row-key="name"
  :options="{ selectable: true }"
>
  <ListRows :rows="rows" />

  <ListSelectBanner>
    <template #actions="{ selections, unselectAll }">
      <Dropdown :options="bulkActions(selections, unselectAll)">
        <Button icon="more-horizontal" variant="ghost" />
      </Dropdown>
    </template>
  </ListSelectBanner>
</ListView>

BULK ACTIONS (EDIT / DELETE)
function bulkActions(selections, unselectAll) {
  return [
    {
      label: 'Edit',
      disabled: selections.length !== 1,
      onClick: () => {
        emit('edit', selections[0].name)
        unselectAll()
      },
    },
    {
      label: 'Delete',
      destructive: true,
      onClick: async () => {
        for (const r of selections) {
          await call('frappe.client.delete', {
            doctype: 'Simple Item',
            name: r.name,
          })
        }
        emit('reload')
        unselectAll()
      },
    },
  ]
}


✔️ Giống CRM Task / Lead 100%

CREATE / EDIT MODAL (DÙNG API CHUẨN)

📍 SimpleItemModal.vue

➕ Create
call('frappe.client.insert', {
  doc: {
    doctype: 'Simple Item',
    ...form.value,
  },
})

✏️ Edit
call('frappe.client.set_value', {
  doctype: 'Simple Item',
  name: form.value.name,
  fieldname: {
    title: form.value.title,
    description: form.value.description,
    quantity: form.value.quantity,
    status: form.value.status,
  },
})


❌ Không viết whitelist
❌ Không get_doc
✔️ CRM dùng cách này

FLOW DỮ LIỆU (CỰC QUAN TRỌNG)
List page load
   ↓
reportview.get
   ↓
rows[]
   ↓
ListView render
   ↓
User select checkbox
   ↓
ListSelectBanner
   ↓
Edit → emit(name)
   ↓
Page set currentItem
   ↓
Modal open
   ↓
Save → insert / set_value
   ↓
emit('saved')
   ↓
items.reload()