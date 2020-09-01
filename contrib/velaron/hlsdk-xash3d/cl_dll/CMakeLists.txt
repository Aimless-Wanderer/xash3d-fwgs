cmake_minimum_required(VERSION 2.8.0)
project(client C CXX)

set(XASH_SDK_CLIENT_SRC_DIR "${XASH_SDK_DIR}/cl_dll")
set(XASH_SDK_CLIENT client)

include(CheckIncludeFile)
check_include_file("tgmath.h" HAVE_TGMATH_H)
if(HAVE_TGMATH_H)
	add_definitions(-DHAVE_TGMATH_H)
endif()

add_definitions(-DCLIENT_WEAPONS -DCLIENT_DLL)
add_definitions(-D_LINUX -DLINUX)
add_definitions(-Dstricmp=strcasecmp -Dstrnicmp=strncasecmp -D_snprintf=snprintf -D_vsnprintf=vsnprintf)

set(XASH_SDK_CLIENT_SRC
	"${XASH_SDK_DIR}/dlls/crossbow.cpp"
	"${XASH_SDK_DIR}/dlls/crowbar.cpp"
	"${XASH_SDK_DIR}/dlls/egon.cpp"
	"${XASH_SDK_DIR}/dlls/gauss.cpp"
	"${XASH_SDK_DIR}/dlls/handgrenade.cpp"
	"${XASH_SDK_DIR}/dlls/hornetgun.cpp"
	"${XASH_SDK_DIR}/dlls/mp5.cpp"
	"${XASH_SDK_DIR}/dlls/python.cpp"
	"${XASH_SDK_DIR}/dlls/rpg.cpp"
	"${XASH_SDK_DIR}/dlls/satchel.cpp"
	"${XASH_SDK_DIR}/dlls/shotgun.cpp"
	"${XASH_SDK_DIR}/dlls/squeakgrenade.cpp"
	"${XASH_SDK_DIR}/dlls/tripmine.cpp"
	"${XASH_SDK_DIR}/dlls/glock.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/ev_hldm.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/hl/hl_baseentity.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/hl/hl_events.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/hl/hl_objects.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/hl/hl_weapons.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/ammo.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/ammo_secondary.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/ammohistory.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/battery.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/cdll_int.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/com_weapons.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/death.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/demo.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/entity.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/ev_common.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/events.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/flashlight.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/GameStudioModelRenderer.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/geiger.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/health.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/hud.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/hud_msg.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/hud_redraw.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/hud_spectator.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/hud_update.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/in_camera.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/input.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/input_goldsource.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/input_mouse.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/input_xash3d.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/menu.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/message.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/overview.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/parsemsg.cpp"
	"${XASH_SDK_DIR}/pm_shared/pm_debug.c"
	"${XASH_SDK_DIR}/pm_shared/pm_math.c"
	"${XASH_SDK_DIR}/pm_shared/pm_shared.c"
	"${XASH_SDK_CLIENT_SRC_DIR}/saytext.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/status_icons.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/statusbar.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/studio_util.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/StudioModelRenderer.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/text_message.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/train.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/tri.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/util.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/view.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/scoreboard.cpp"
	"${XASH_SDK_CLIENT_SRC_DIR}/MOTD.cpp"
)

include_directories(
	"${XASH_SDK_CLIENT_SRC_DIR}/"
	"${XASH_SDK_CLIENT_SRC_DIR}/hl"
	"${XASH_SDK_DIR}/dlls"
	"${XASH_SDK_DIR}/dlls/wpn_shared"
	"${XASH_SDK_DIR}/common"
	"${XASH_SDK_DIR}/engine"
	"${XASH_SDK_DIR}/pm_shared"
	"${XASH_SDK_DIR}/game_shared"
	"${XASH_SDK_DIR}/public"
	"${XASH_SDK_DIR}/utils/false_vgui/include"
)

add_library (${XASH_SDK_CLIENT} MODULE ${XASH_SDK_CLIENT_SRC})
