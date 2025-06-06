# SPDX-License-Identifier: Apache-2.0

add_subdirectory_ifdef(CONFIG_BT_SHELL shell)

zephyr_library()

zephyr_library_sources(audio.c)

if (CONFIG_BT_VOCS OR CONFIG_BT_VOCS_CLIENT)
	zephyr_library_sources(vocs.c)
endif()
zephyr_library_sources_ifdef(CONFIG_BT_VOCS_CLIENT vocs_client.c)

if (CONFIG_BT_AICS OR CONFIG_BT_AICS_CLIENT)
	zephyr_library_sources(aics.c)
endif()
zephyr_library_sources_ifdef(CONFIG_BT_AICS_CLIENT aics_client.c)

zephyr_library_sources_ifdef(CONFIG_BT_VCP_VOL_REND vcp_vol_rend.c)
zephyr_library_sources_ifdef(CONFIG_BT_VCP_VOL_CTLR vcp_vol_ctlr.c)

if (CONFIG_BT_MICP_MIC_DEV)
	zephyr_library_sources(micp_mic_dev.c)
endif()
zephyr_library_sources_ifdef(CONFIG_BT_MICP_MIC_CTLR micp_mic_ctlr.c)

# When CONFIG_BT_AUDIO and CONFIG_BT_CONN is enabled we pull in ccid. It is based on CONFIG_BT_CONN
# as CCID depends on GATT, and GATT is enabled when CONFIG_BT_CONN=y.
zephyr_library_sources_ifdef(CONFIG_BT_CONN ccid.c)

zephyr_library_link_libraries(subsys__bluetooth)

zephyr_library_sources_ifdef(CONFIG_BT_CSIP_SET_MEMBER csip_set_member.c)
zephyr_library_sources_ifdef(CONFIG_BT_CSIP_SET_COORDINATOR csip_set_coordinator.c)
if (CONFIG_BT_CSIP_SET_MEMBER OR CONFIG_BT_CSIP_SET_COORDINATOR)
	zephyr_library_sources(csip_crypto.c)
endif()

zephyr_library_sources_ifdef(CONFIG_BT_TBS tbs.c)

zephyr_library_sources_ifdef(CONFIG_BT_TBS_CLIENT tbs_client.c)

zephyr_library_sources_ifdef(CONFIG_BT_MCC mcc.c)

zephyr_library_sources_ifdef(CONFIG_BT_MCS mcs.c)

zephyr_library_sources_ifdef(CONFIG_BT_MPL mpl.c)

zephyr_library_sources_ifdef(CONFIG_MCTL media_proxy.c)

zephyr_library_sources_ifdef(CONFIG_BT_ASCS ascs.c)
zephyr_library_sources_ifdef(CONFIG_BT_PACS pacs.c)
zephyr_library_sources_ifdef(CONFIG_BT_BAP_STREAM bap_stream.c codec.c bap_iso.c)
zephyr_library_sources_ifdef(CONFIG_BT_BAP_BASE bap_base.c)
zephyr_library_sources_ifdef(CONFIG_BT_BAP_UNICAST_SERVER bap_unicast_server.c)
zephyr_library_sources_ifdef(CONFIG_BT_BAP_UNICAST_CLIENT bap_unicast_client.c)
zephyr_library_sources_ifdef(CONFIG_BT_BAP_BROADCAST_SOURCE bap_broadcast_source.c)
zephyr_library_sources_ifdef(CONFIG_BT_BAP_BROADCAST_SINK bap_broadcast_sink.c)
zephyr_library_sources_ifdef(CONFIG_BT_BAP_SCAN_DELEGATOR bap_scan_delegator.c)
zephyr_library_sources_ifdef(CONFIG_BT_BAP_BROADCAST_ASSISTANT bap_broadcast_assistant.c)
zephyr_library_sources_ifdef(CONFIG_BT_CCP_CALL_CONTROL_CLIENT ccp_call_control_client.c)
zephyr_library_sources_ifdef(CONFIG_BT_CCP_CALL_CONTROL_SERVER ccp_call_control_server.c)
zephyr_library_sources_ifdef(CONFIG_BT_HAS has.c)
zephyr_library_sources_ifdef(CONFIG_BT_HAS_CLIENT has_client.c)
zephyr_library_sources_ifdef(CONFIG_BT_CAP cap_stream.c)
zephyr_library_sources_ifdef(CONFIG_BT_CAP_ACCEPTOR cap_acceptor.c)
zephyr_library_sources_ifdef(CONFIG_BT_CAP_INITIATOR cap_initiator.c)
zephyr_library_sources_ifdef(CONFIG_BT_CAP_COMMANDER cap_commander.c)
if (CONFIG_BT_CAP_INITIATOR_UNICAST OR CONFIG_BT_CAP_COMMANDER)
	zephyr_library_sources(cap_common.c)
endif()
zephyr_library_sources_ifdef(CONFIG_BT_TMAP tmap.c)
zephyr_library_sources_ifdef(CONFIG_BT_GMAP gmap_client.c gmap_server.c)
zephyr_library_sources_ifdef(CONFIG_BT_PBP pbp.c)
