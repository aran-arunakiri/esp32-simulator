set(LWIP_SOURCES
	"core/altcp_alloc.c"
	"core/altcp.c"
	"core/altcp_tcp.c"
	"core/def.c"
	"core/dns.c"
	"core/inet_chksum.c"
	"core/init.c"
	"core/ip.c"
	"core/ipv4"
	"core/ipv6"
	"core/mem.c"
	"core/memp.c"
	"core/netif.c"
	"core/pbuf.c"
	"core/raw.c"
	"core/stats.c"
	"core/sys.c"
	"core/tcp.c"
	"core/tcp_in.c"
	"core/tcp_out.c"
	"core/timeouts.c"
	"core/udp.c"

	"core/ipv4/autoip.c"
	"core/ipv4/dhcp.c"
	"core/ipv4/etharp.c"
	"core/ipv4/icmp.c"
	"core/ipv4/igmp.c"
	"core/ipv4/ip4_addr.c"
	"core/ipv4/ip4.c"
	"core/ipv4/ip4_frag.c"

	"core/ipv6/dhcp6.c"
	"core/ipv6/ethip6.c"
	"core/ipv6/icmp6.c"
	"core/ipv6/inet6.c"
	"core/ipv6/ip6_addr.c"
	"core/ipv6/ip6.c"
	"core/ipv6/ip6_frag.c"
	"core/ipv6/mld6.c"
	"core/ipv6/nd6.c"

	"api/api_lib.c"
	"api/api_msg.c"
	"api/err.c"
	"api/if_api.c"
	"api/netbuf.c"
	"api/netdb.c"
	"api/netifapi.c"
	"api/sockets.c"
	"api/tcpip.c"

	"netif/bridgeif.c"
	"netif/bridgeif_fdb.c"
	"netif/ethernet.c"
	"netif/lowpan6_ble.c"
	"netif/lowpan6.c"
	"netif/lowpan6_common.c"
	"netif/slipif.c"
	"netif/zepif.c"

	"netif/ppp/auth.c"
	"netif/ppp/ccp.c"
	"netif/ppp/demand.c"
	"netif/ppp/eap.c"
	"netif/ppp/ecp.c"
	"netif/ppp/eui64.c"
	"netif/ppp/fsm.c"
	"netif/ppp/chap-md5.c"
	"netif/ppp/chap_ms.c"
	"netif/ppp/chap-new.c"
	"netif/ppp/ipcp.c"
	"netif/ppp/ipv6cp.c"
	"netif/ppp/lcp.c"
	"netif/ppp/magic.c"
	"netif/ppp/mppe.c"
	"netif/ppp/multilink.c"
	"netif/ppp/pppapi.c"
	"netif/ppp/ppp.c"
	"netif/ppp/pppcrypt.c"
	"netif/ppp/pppoe.c"
	"netif/ppp/pppol2tp.c"
	"netif/ppp/pppos.c"
	"netif/ppp/upap.c"
	"netif/ppp/utils.c"
	"netif/ppp/vj.c"

	"netif/ppp/polarssl/arc4.c"
	"netif/ppp/polarssl/des.c"
	"netif/ppp/polarssl/md4.c"
	"netif/ppp/polarssl/md5.c"
	"netif/ppp/polarssl/sha1.c"
)
set(LWIP_CONTRIB
	"ports/freertos/sys_arch.c"
	"ports/unix/port/netif/sio.c"
)
include_directories(
	"${CMAKE_CURRENT_SOURCE_DIR}/extra"
	"${CMAKE_CURRENT_SOURCE_DIR}/src/src/include"
	"${CMAKE_CURRENT_SOURCE_DIR}/contrib/ports/freertos/include"
	"${CMAKE_CURRENT_SOURCE_DIR}/contrib/ports/unix/port/include"
	${ESP_SIMULATOR_INCLUDE_DIRECTORIES}
	"${ESP_CONFIG_DIR}"
)

list(TRANSFORM LWIP_SOURCES PREPEND ${CMAKE_CURRENT_SOURCE_DIR}/src/src/)
list(TRANSFORM LWIP_CONTRIB PREPEND ${CMAKE_CURRENT_SOURCE_DIR}/contrib/)
add_definitions(-DDEFAULT_THREAD_STACKSIZE=1024 -DTCPIP_THREAD_STACKSIZE=1024 -g3 -ggdb)
add_library(lwip STATIC
	${LWIP_SOURCES}
	${LWIP_CONTRIB}
	"${CMAKE_CURRENT_SOURCE_DIR}/extra/tapif.c"
)
