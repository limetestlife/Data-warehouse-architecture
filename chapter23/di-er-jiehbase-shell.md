## Group name: 基础信息
  Commands: status, table_help, version, whoami
包括查看系统状态，版本，用户等等
## Group name: ddl
Commands: alter, alter_async, alter_status, create, describe, disable, disable_all, drop, drop_all, enable, enable_all, exists, get_table, is_disabled, is_enabled, list, locate_region, show_filters
表定义指令，包括创建表，删除表，查看表，查看表状态等等　
　
## Group name: namespace
  Commands: alter_namespace, create_namespace, describe_namespace, drop_namespace, list_namespace, list_namespace_tables
和namespace相关的指令，包括创建，删除，显示结构，列出，修改，列出namespace下的表等等

## Group name: dml
Commands: append, count, delete, deleteall, get, get_counter, get_splits, incr, put, scan, truncate, truncate_preserve
表管理指令，包括追加，计数，删除，获取，添加，浏览，清空数据等等

## Group name: tools
  Commands: assign, balance_switch, balancer, balancer_enabled, catalogjanitor_enabled, catalogjanitor_run, catalogjanitor_switch, close_region, compact, compact_mob, compact_rs, flush, major_compact, major_compact_mob, merge_region, move, normalize, normalizer_enabled, normalizer_switch, split, trace, unassign, wal_roll, zk_dump

## Group name: replication
  Commands: add_peer, append_peer_tableCFs, disable_peer, disable_table_replication, enable_peer, enable_table_replication, list_peers, list_replicated_tables, remove_peer, remove_peer_tableCFs, set_peer_tableCFs, show_peer_tableCFs

## Group name: snapshots
  Commands: clone_snapshot, delete_all_snapshot, delete_snapshot, list_snapshots, restore_snapshot, snapshot

## Group name: configuration
  Commands: update_all_config, update_config
## Group name: quotas
  Commands: list_quotas, set_quota

## Group name: security
  Commands: grant, list_security_capabilities, revoke, user_permission
表权限管理，安全管理 ，包括授权，收回，查看权限等等

## Group name: procedures
  Commands: abort_procedure, list_procedures

## Group name: visibility labels
  Commands: add_labels, clear_auths, get_auths, list_labels, set_auths, set_visibility