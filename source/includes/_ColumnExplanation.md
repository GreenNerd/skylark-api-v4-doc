# Column Explanation

下文各接口的嵌套对象使用这里的字段。示例里的手机号、openid 和链接都是占位值。

## 用户

v4 用户列表和详情（`api/v4/users/_user`）在精简字段上增加 `tags`、`organizations`、`profile_submission`。

精简用户字段：`id`、`name`、`nickname`、`sex`、`phone`、`identifier`、`openid`、`binded_at`、`headimgurl`、`created_at`、`updated_at`。

`tags` 只有 `id`、`name`。`organizations` 只有 `id`、`name`、`description`、`created_at`。

组织成员接口的用户另有 `tag_ids`，其 `tags` 为 `id`、`name`、`full_name`，没有 `headimgurl`。

评论作者、帖子作者、组织管理员里的用户来自后台模板，字段是 `id`、`name`、`nickname`、`phone`、`identifier`、`qq`、`headimgurl`、`openid`、`imported_alias`、`from_wechat`，标签含 `color`、`tag_group_id`、`taggings_count`。

Mapper 用户：`id`、`name`、`nickname`、`sex`、`phone`、`identifier`、`openid`、`created_at`、`updated_at`。

## 组织

`id`、`name`、`description`、`description_text`、`created_at`、`updated_at`、`children_count`、`parent_id`、`ancestry`、`ancestor_names`、`application_strategy`。

`application_strategy`：`must_approved`、`auto_approved`、`closed`。

有资料时附带 `profile_submission.entries` 与 `profile_submission.cached_values`。

`GET /organizations/:id` 再附加 `apply_link`、`members_count`、`binded_members_count`、`pending_organization_applications_count`。

用户的「所在组织」接口只返回 `id`、`name`、`description`、`description_text`、`created_at`、`updated_at`、`children_count`、`parent_id`、`ancestry`。

## 标签

v4 标签：`id`、`name`、`full_name`。

标签组：`id`、`name`、`type`、`namespace_id`。`type` 为 `user`、`receipt` 或 `yaw`。

## 附件

`id`、`name`、`size`、`mime_type`、`extension`、`extra_info`、`download_url`。

`download_url` 会带上请求里的 `fops` 或 `variant`。七牛环境下 `fops` 走图片处理；其他存储后端可能走 `variant`。

## 条目 Entry

`id`、`field_id`、`option_id`、`value`、`choice_id`、`value_id`、`latitude`、`longitude`、`group_id`、`detail_id`。

有附件时附带附件对象。级联字段附带 `choice`（`id`、`name`、`ancestry`、`parent_id`、`locked`、`children_count`），没有选项时 `choice` 为 `null`。

写入时放在 `entries_attributes` 或 `response[entries_attributes]`，可传字段：

`id`、`value`、`field_id`、`option_id`、`choice_id`、`value_id`、`longitude`、`latitude`、`_destroy`、`group_id`。表单记录的更新还接受 `slp_index`。

## 字段 Field

`id`、`title`、`description`、`type`、`position`、`validations`、`other_option`、`visibility`、`marked`、`settings`、`detail_id`、`identity_key`、`data`、`maximum`。

明细字段有 `children`。级联字段有 `cascaded_select`（`id`、`name`、`labels`、`locked`、`min_label_length`、`choices`）。可选项字段有 `options`：`id`、`value`、`settings`、`position`。

创建或更新表单、流程时，`fields_attributes` 可传：

`title`、`description`、`type`、`other_option`、`position`、`visibility`、`marked`、`cascaded_select_id`、`maximum`、`longitude`、`latitude`、`max_distance`、`remark`、`value_cache`、`slp_index`、`identity_key`、`validations`、`data[execed_js]`、`settings`（含 `adjust_radius`、`layout`、`input_type`、`button_name`、`callback_url`、`register_writed`、`presence`、`explicit`、`enable_modify`、`only_leaf`、`location_watermark`、`datetime_watermark`、`other_option_settings`、`length_limit`、`char_size_limit_settings`、`limit_settings`）、`options_attributes`（`value`、`slp_index`、`position`、`settings`）、`children_attributes`（同样的一套）。

更新时每个字段和选项还可以传 `id`、`_destroy`。

## 可见范围 user_boundary

`id`、`organization_ids`、`user_tag_ids`、`user_tagged_type`、`only_binded`、`overlord_type`、`overlord_id`、`created_at`、`updated_at`、`namespace_id`、`user_ids`、`status`、`append_count`、`cached_organization_ids`、`cached_user_ids`、`extra_boundary`、`type`。

写入时：`only_binded`、`user_tagged_type`、`user_tag_ids`、`user_ids`、`organization_ids`。

## 表单记录 Response

`id`、`created_at`、`updated_at`、`cached_values`、`mapped_values`、`involved_user_ids`、`involved_organization_ids`、`entries`、`user`。

Mapper 的记录没有 `entries`，用户是 Mapper 用户。

## cached_values

展示用 `text_value`。附件地址有时效，长期下载走附件接口。

普通字段：

```json
{
  "12": {
    "value": ["示例"],
    "text_value": ["示例"],
    "exported_value": ["示例"]
  }
}
```

明细字段：

```json
{
  "30": {
    "group_ids": [1],
    "child_ids": [31]
  }
}
```

明细内字段：

```json
{
  "31": {
    "grouped_ids": [1],
    "grouped_values": [
      {
        "group_id": 1,
        "value": ["示例"],
        "text_value": ["示例"],
        "exported_value": ["示例"]
      }
    ]
  }
}
```

## 搜索用的虚拟字段 id

表单记录搜索（`query` 的键会转成整数）：

| id | 含义 |
| --- | --- |
| 表单字段 id | 该字段的值 |
| -1 | 创建时间 |
| -2 | 用户 |
| -3 | 组织 |
| -18 | 用户标识 |
| -20 | 手机号 |

`order` 只取第一对：字段 id 到 `asc` 或 `desc`。

流程 journey 搜索额外识别：

| id | 含义 |
| --- | --- |
| -4 | 任务时限 |
| -5 | 流程单号 |
| -6 | 流程状态 |
| -7 | 流程时限 |
| -8 | 节点名称 |
| -9 | 任务状态 |
| -12 | 流程创建时间 |
| -13 | 发起人 |
| -19 | 发起人标识 |
| -25 | 自定义单号 |

以及该流程可搜索的表单字段 id。

## 流程对象

### Flow

`id`、`title`、`html_body`、`external_settings`、`identity_vertify_type`、`logic_settings`、`fields`。不带 `slim` 时还有 `vertices`、`edges`、`graphs`。

节点：`id`、`name`、`type`、`field_ids`、`operations`、`settings`、`logic_settings`、`metadata`、`alias_name`、`graph_id`、`push_settings`、`in_edges`、`out_edges`、`fields`、`user_boundary`、`cc_user_boundary`。节点名称是 `name`。

边：`id`、`from_vertex_id`、`to_vertex_id`、`metadata`、`flow_id`、`graph_id`、`conditions_count`、`deleted_at`、`created_at`、`updated_at`、`conditions`（`id`、`position`、`conditionable_type`、`conditionable_id`、`judgements`、`edge_id`、`created_at`、`updated_at`）。

图：`id`、`created_at`、`updated_at`、`metadata`、`ancestry`、`ancestry_depth`、`flow_id`、`name`、`settings`、`active_errors`。

用户可见流程列表返回的是缓存计数：`id`、`user_id`、`flow_id`、`flow_title`、`proposed_uncompleted_assignments_count`、`processed_uncompleted_assignments_count`、`cc_uncompleted_assignments_count`、`created_at`、`updated_at`。

### Journey

`id`、`sn`、`status`、`current_duration_threshold`、`flow_id`、`created_at`、`updated_at`、`current_vertex_id`、`reviewer_vertex_ids`、`journey_url`、`response`、`user`（精简用户）、`hourglasses`。

嵌套的 `response` 是 `id`、`cached_values`、`mapped_values`、`entries`。

`GET .../journeys/new` 再附带 `assignments`。

### Assignment

v4 列表里的任务：`id`、`assignee_id`、`status`、`category`、`read`、`operation_data`、`current_duration_threshold`、`vertex_id`、`journey_id`、`created_at`、`updated_at`、`response`、`hourglasses`。

`category`：`proposed` 发起人，`processed` 处理人，`cc` 抄送。

`operation_data` 里常见：`comment`、`esignature`、`next_vertex_id`、`next_reviewer_ids`、`duration_thresholds`、`carbon_copy_user_ids`。

发起或审批成功时，返回的是后台任务模板，根字段包括 `id`、`status`、`category`、`read`、`current_duration_threshold`、`created_at`、`updated_at`、`after_submit_action`、`after_submit_redirect_url`、`gid`、`pretty_current_duration_threshold`、`journey`、`response`。`operation` 为 `route` 时外面再包一层：

`assignment`、`next_vertices`（`id`、`name`、`type`、`metadata`、`operations`、`settings`、`graph_id`、`logic_settings`、`automatic`、`created_at`、`updated_at`、`gid`、`fields`）、`next_graphs`（`id`、`name`、`ancestry`、`settings`、`metadata`、`created_at`、`updated_at`、`gid`）。

### Moment

`id`、`status`、`comment`、`esignature`、`vertex_id`、`journey_id`、`flow_id`、`created_at`、`updated_at`、`assignment`、`user`。

`category` 和 `operation_data` 属于 Assignment，不属于 Moment。

### Hourglass

`id`、`status`、`agendable_type`、`agendable_id`、`journey_id`、`alert_at`、`assigner_id`、`assignment_in_charge_id`。

### 延期申请

`id`、`status`、`requester_id`、`requester_assignment_id`、`assignment_id`、`data`、`hourglass_id`、`approve_result_alert_at`、`moment_id`、`created_at`、`updated_at`。

## 流程状态

发起时为发起人创建 `proposed` 任务。到达处理节点时为每个处理人创建 `processed` 任务。发起人任务的状态与 Journey 同步。全部节点通过后 Journey 为 `finished`。拒绝回开始节点后 Journey 为 `receding`。

处理人任务状态：`processing`、`approved`、`refused`、`transferred`、`skipped`。

发起人任务状态：`processing`、`cancelled`、`receding`、`finished`、`aborted`、`suspended`。

## 评论

`id`、`author_id`、`commentable_id`、`commentable_type`、`body`、`status`、`handled_user_id`、`replied_comment_id`、`created_at`、`author`（后台用户对象）。

可评论对象参数名：`form_id`、`post_id`、`cms_page_id`、`template_post_id`。
