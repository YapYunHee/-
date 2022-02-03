function SearchWrite(Search, Write, Type)
    gg.clearResults()
    gg.setVisible(false)
    gg.searchNumber(Search[1][1], Type)
    local count = gg.getResultCount()
    local result = gg.getResults(count)
    gg.clearResults()
    local data = {} 
    local base = Search[1][2] 
    
   if (count > 0) then
        for i, v in ipairs(result) do
            v.isUseful = true 
        end
        
        for k=2, #Search do
            local tmp = {}
            local offset = Search[k][2] - base 
            local num = Search[k][1] 
            
            for i, v in ipairs(result) do
                tmp[#tmp+1] = {} 
                tmp[#tmp].address = v.address + offset  
                tmp[#tmp].flags = v.flags  
            end
            
            tmp = gg.getValues(tmp) 
            
            for i, v in ipairs(tmp) do
                if ( tostring(v.value) ~= tostring(num) ) then 
                    result[i].isUseful = false
                end
            end
        end
  
        for i, v in ipairs(result) do
            if (v.isUseful) then 
                data[#data+1] = v.address
            end
        end
       
        if (#data > 0) then
           gg.toast("搜索到"..#data.."条数据")
           local t = {}
           local base = Search[1][2]
           for i=1, #data do
               for k, w in ipairs(Write) do
                   offset = w[2] - base
                   t[#t+1] = {}
                   t[#t].address = data[i] + offset
                   t[#t].flags = Type
                   t[#t].value = w[1]
                  
                   if (w[3] == true) then
                       local item = {}
                       item[#item+1] = t[#t]
                       item[#item].freeze = true
                       gg.addListItems(item)
                   end
                   
               end
           end
           gg.setValues(t)
        
        else
            gg.toast("not found", false)
            return false
        end
    else
        gg.toast("未搜到任何数据")
        return false
    end
end
function split(szFullString, szSeparator) local nFindStartIndex = 1 local nSplitIndex = 1 local nSplitArray = {} while true do local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex) if not nFindLastIndex then nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString)) break end nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1) nFindStartIndex = nFindLastIndex + string.len(szSeparator) nSplitIndex = nSplitIndex + 1 end return nSplitArray end function xgxc(szpy, qmxg) for x = 1, #(qmxg) do xgpy = szpy + qmxg[x]["offset"] xglx = qmxg[x]["type"] xgsz = qmxg[x]["value"] gg.setValues({[1] = {address = xgpy, flags = xglx, value = xgsz}}) xgsl = xgsl + 1 end end function xqmnb(qmnb) gg.clearResults() gg.setRanges(qmnb[1]["memory"]) gg.searchNumber(qmnb[3]["value"], qmnb[3]["type"]) if gg.getResultCount() == 0 then gg.toast(qmnb[2]["name"] .. "开启失败") else gg.refineNumber(qmnb[3]["value"], qmnb[3]["type"]) gg.refineNumber(qmnb[3]["value"], qmnb[3]["type"]) gg.refineNumber(qmnb[3]["value"], qmnb[3]["type"]) if gg.getResultCount() == 0 then gg.toast(qmnb[2]["name"] .. "开启失败") else sl = gg.getResults(999999) sz = gg.getResultCount() xgsl = 0 if sz > 999999 then sz = 999999 end for i = 1, sz do pdsz = true for v = 4, #(qmnb) do if pdsz == true then pysz = {} pysz[1] = {} pysz[1].address = sl[i].address + qmnb[v]["offset"] pysz[1].flags = qmnb[v]["type"] szpy = gg.getValues(pysz) pdpd = qmnb[v]["lv"] .. ";" .. szpy[1].value szpd = split(pdpd, ";") tzszpd = szpd[1] pyszpd = szpd[2] if tzszpd == pyszpd then pdjg = true pdsz = true else pdjg = false pdsz = false end end end if pdjg == true then szpy = sl[i].address xgxc(szpy, qmxg) xgjg = true end end if xgjg == true then gg.toast(qmnb[2]["name"] .. "开启成功,共修改" .. xgsl .. "条数据") else gg.toast(qmnb[2]["name"] .. "开启失败") end end end end
function SearchWrite(Search, Write, Type, Name) gg.clearResults() gg.setVisible(false) gg.searchNumber(Search[1][1], Type)local count = gg.getResultCount()local result = gg.getResults(count) gg.clearResults()local data = {}local base = Search[1][2]if (count > 0)then for i, v in ipairs(result)do v.isUseful =true end for k=2, #Search do local tmp = {}local offset = Search[k][2] - base local num = Search[k][1]for i, v in ipairs(result)do tmp[#tmp+1] = {} tmp[#tmp].address = v.address + offset tmp[#tmp].flags = v.flags end tmp = gg.getValues(tmp)for i, v in ipairs(tmp)do if ( tostring(v.value) ~= tostring(num) )then result[i].isUseful =false end end end for i, v in ipairs(result)do if (v.isUseful)then data[#data+1] = v.address end end if (#data > 0)then gg.toast("搜索到"..#data.."條數據")local t = {}local base = Search[1][2]for i=1, #data do for k, w in ipairs(Write)do offset = w[2] - base t[#t+1] = {} t[#t].address = data[i] + offset t[#t].flags = Type t[#t].value = w[1]if (w[3] == true)then local item = {} item[#item+1] = t[#t] item[#item].freeze =true gg.addListItems(item)end end end gg.setValues(t) gg.toast(Name.."已修改"..#t.."條數據") gg.addListItems(t)else gg.toast(Name.."開啟失敗", false)return false end else gg.toast(Name.."開啟失敗")return false end end
function split(szFullString, szSeparator) local nFindStartIndex = 1 local nSplitIndex = 1 local nSplitArray = {} while true do local nFindLastIndex = string.find(szFullString, szSeparator, nFindStartIndex) if not nFindLastIndex then nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, string.len(szFullString)) break end nSplitArray[nSplitIndex] = string.sub(szFullString, nFindStartIndex, nFindLastIndex - 1) nFindStartIndex = nFindLastIndex + string.len(szSeparator) nSplitIndex = nSplitIndex + 1 end return nSplitArray end function xgxc(szpy, qmxg) for x = 1, #(qmxg) do xgpy = szpy + qmxg[x]["offset"] xglx = qmxg[x]["type"] xgsz = qmxg[x]["value"] gg.setValues({[1] = {address = xgpy, flags = xglx, value = xgsz}}) xgsl = xgsl + 1 end end function xqmnb(qmnb) gg.clearResults() gg.setRanges(qmnb[1]["memory"]) gg.searchNumber(qmnb[3]["value"], qmnb[3]["type"]) if gg.getResultCount() == 0 then gg.toast(qmnb[2]["name"] .. "開啟失敗") else gg.refineNumber(qmnb[3]["value"], qmnb[3]["type"]) gg.refineNumber(qmnb[3]["value"], qmnb[3]["type"]) gg.refineNumber(qmnb[3]["value"], qmnb[3]["type"]) if gg.getResultCount() == 0 then gg.toast(qmnb[2]["name"] .. "開啟失敗") else sl = gg.getResults(999999) sz = gg.getResultCount() xgsl = 0 if sz > 999999 then sz = 999999 end for i = 1, sz do pdsz = true for v = 4, #(qmnb) do if pdsz == true then pysz = {} pysz[1] = {} pysz[1].address = sl[i].address + qmnb[v]["offset"] pysz[1].flags = qmnb[v]["type"] szpy = gg.getValues(pysz) pdpd = qmnb[v]["lv"] .. ";" .. szpy[1].value szpd = split(pdpd, ";") tzszpd = szpd[1] pyszpd = szpd[2] if tzszpd == pyszpd then pdjg = true pdsz = true else pdjg = false pdsz = false end end end if pdjg == true then szpy = sl[i].address xgxc(szpy, qmxg) xgjg = true end end if xgjg == true then gg.toast(qmnb[2]["name"] .. "開啟成功,共修改" .. xgsl .. "條數據") else gg.toast(qmnb[2]["name"] .. "開啟失敗") end end end end
function SearchWrite(Search, Write, Type) gg.clearResults() gg.setVisible(false) gg.searchNumber(Search[1][1], Type) local count = gg.getResultCount() local result = gg.getResults(count) gg.clearResults() local data = {} local base = Search[1][2] if (count > 0) then for i, v in ipairs(result) do v.isUseful = true end for k=2, #Search do local tmp = {} local offset = Search[k][2] - base local num = Search[k][1] for i, v in ipairs(result) do tmp[#tmp+1] = {} tmp[#tmp].address = v.address + offset tmp[#tmp].flags = v.flags end tmp = gg.getValues(tmp) for i, v in ipairs(tmp) do if ( tostring(v.value) ~= tostring(num) ) then result[i].isUseful = false end end end for i, v in ipairs(result) do if (v.isUseful) then data[#data+1] = v.address end end if (#data > 0) then local t = {} local base = Search[1][2] for i=1, #data do for k, w in ipairs(Write) do offset = w[2] - base t[#t+1] = {} t[#t].address = data[i] + offset t[#t].flags = Type t[#t].value = w[1] if (w[3] == true) then local item = {} item[#item+1] = t[#t] item[#item].freeze = true gg.addListItems(item) end end end gg.setValues(t) gg.addListItems(t) else gg.toast("无数据", false) return false end else gg.toast("Not Found") return false end end
function RGD() end
function setvalue(address,flags,value) RGD('Modify address value (address, value type, value to be modified)') local tt={} tt[1]={} tt[1].address=address tt[1].flags=flags tt[1].value=value gg.setValues(tt) end

MrTeamz=gg


HOMEDM = 1
function HOME()
YZ = gg.choice({

" 内存防封️ ✧ \n ╰〖 游戏大厅 〗",
" 自动飞天 ✧ \n ╰〖 游戏内开 〗",
" 排位菜单️ ✧ \n ╰〖 游戏内开 〗",
" 墙射菜单 ✧ \n ╰〖 大厅内开 〗",
" 挑战菜单️ ✧ \n ╰〖 游戏内开 〗",
" 上色菜单️ ✧ \n ╰〖 游戏内开 〗",
" 飞天遁地️ ✧ \n ╰〖 游戏内开 〗",
" 子弹追踪 ✧ \n ╰〖 游戏内开 〗",
"  XA功能   ✧ \n ╰〖 大厅内开 〗",
" 退出脚本️ ✧ "
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if YZ == nil then
NOSELECT()
else
if YZ == 1 then A() end
if YZ == 2 then B() end
if YZ == 3 then C() end
if YZ == 4 then D() end
if YZ == 5 then E() end
if YZ == 6 then F() end
if YZ == 7 then G() end
if YZ == 8 then H() end
if YZ == 9 then I() end
if YZ == 10 then CLOSE() end
end
HOMEDM = -1
end

function NOSELECT()
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_00")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_01")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_02")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_03")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_04")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_05")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_06")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_07")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_tombstones/tombstone_00")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_tombstones/tombstone_01")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_tombstones/tombstone_02")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_tombstones/tombstone_03")
gg.toast(os.date("༆ 叶仔辅助‖当前时间: %H:%M:%S %Z ༄"))
end

function A()
menu1 = gg.multiChoice({
'内存防封',
'清除数据',
'防举报',
'返回大厅'},
nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if menu1 == nil then HOME() else
if menu1[1] == true then d1() end
if menu1[2] == true then d2() end
if menu1[3] == true then d3() end
if menu1[4] == true then HOME() end
end
HOMEDM = -1
end

function d1()
MrTeamz.setRanges(16384)
MrTeamz.clearResults()
MrTeamz.searchNumber("10,824.0087890625",4)
MrTeamz.getResults(5000)
MrTeamz.editAll("0",4)
MrTeamz.clearResults()
MrTeamz.setRanges(16384)
MrTeamz.clearResults()
MrTeamz.searchNumber("123,328.1875",4)
MrTeamz.getResults(5000)
MrTeamz.editAll("0",4)
MrTeamz.clearResults()
MrTeamz.setRanges(16384)
MrTeamz.clearResults()
MrTeamz.searchNumber("123,328.1875",4)
MrTeamz.getResults(5000)
MrTeamz.editAll("0",4)
MrTeamz.clearResults()
MrTeamz.setRanges(16384)
MrTeamz.clearResults()
MrTeamz.searchNumber("123,328.1875",4)
MrTeamz.getResults(5000)
MrTeamz.editAll("0",4)
MrTeamz.clearResults()
MrTeamz.setRanges(16384)
MrTeamz.clearResults()
MrTeamz.searchNumber("17,728.193359375",4)
MrTeamz.getResults(5000)
MrTeamz.editAll("0",4)
MrTeamz.clearResults()
MrTeamz.setRanges(16384)
MrTeamz.clearResults()
MrTeamz.searchNumber("17,728.193359375",4)
MrTeamz.getResults(5000)
MrTeamz.editAll("0",4)
MrTeamz.clearResults()
MrTeamz.setRanges(16384)
MrTeamz.clearResults()
MrTeamz.searchNumber("123,328.1875",4)
MrTeamz.getResults(5000)
MrTeamz.editAll("0",4)
MrTeamz.clearResults()
MrTeamz.setRanges(16384)
MrTeamz.clearResults()
MrTeamz.searchNumber("123,328.1875",4)
MrTeamz.getResults(5000)
MrTeamz.editAll("0",4)
MrTeamz.setRanges(16384)
MrTeamz.clearResults()
MrTeamz.searchNumber("123,328.1875",4)
MrTeamz.getResults(5000)
MrTeamz.editAll("0",4)
MrTeamz.clearResults()
MrTeamz.alert("内存防封开启成功")
end



function d2()
os.remove("/storage/emulated/0/Android/data/com.dkgame.gplay.crisisactiontw/files/AntiCheatEngineLog.txt")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/gameplugins/com.dkgame.gplay.crisisactiontw/files/commonex14")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/gameplugins/com.dkgame.gplay.crisisactiontw/files/fightex14")
os.remove("/storage/emulated/0/Android/data/com.dkgame.gplay.crisisactiontw/files/AntiCheatEngineLog.txt")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_00")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_01")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_02")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_03")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_04")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_05")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_06")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_logs/log_07")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_tombstones/tombstone_00")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_tombstones/tombstone_01")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_tombstones/tombstone_02")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/files/lb_tombstones/tombstone_03")
os.remove("/storage/emulated/0/Android/data/com.dkgame.gplay.crisisactiontw/files/AntiCheatEngineLog.txt")
os.remove("/storage/emulated/0/Android/data/com.yunz.fsds/gameplugins/com.dkgame.gplay.crisisactiontw/files/AntiCheatEngineLog.txt")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_logs/log_00")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_logs/log_01")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_logs/log_02")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_logs/log_03")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_logs/log_04")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_logs/log_05")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_logs/log_06")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_logs/log_07")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_tombstones/tombstone_00")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_tombstones/tombstone_01")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_tombstones/tombstone_02")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/files/lb_tombstones/tombstone_03")
os.remove("/storage/emulated/0/Android/data/com.herogames.gplay.crisisactionsa/files/AntiCheatEngineLog.txt")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/gameplugins/com.herogames.gplay.crisisactionsa/files/AntiCheatEngineLog.txt")
os.remove("/storage/emulated/0/Android/data/com.herogames.gplay.crisisactionsa/files/AntiCheatEngineLog.txt")
os.remove("/storage/emulated/0/Android/data/com.excean.parallelspace.b32/gameplugins/com.herogames.gplay.crisisactionsa/files/AntiCheatEngineLog.txt")
MrTeamz.toast("已清除数据")
end

function d3()
gg.setRanges(16384)
gg.clearResults()
gg.searchNumber(":hack", gg.TYPE_BYTE, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100000)
gg.editAll("0", gg.TYPE_BYTE)
gg.clearResults()
gg.searchNumber(":bann", gg.TYPE_BYTE, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100000)
gg.editAll("0", gg.TYPE_BYTE)
gg.clearResults()
gg.searchNumber(":anti", gg.TYPE_BYTE, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100000)
gg.editAll("0", gg.TYPE_BYTE)
gg.clearResults()
gg.searchNumber(":report", gg.TYPE_BYTE, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(200, nil, nil, nil, nil, nil, nil, nil, nil)
gg.editAll("0", gg.TYPE_BYTE)
gg.clearResults()
so=gg.getRangesList('libunity.so')[1].start
py=0xa199f4
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0xa19a94
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0xa19b34
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0xa19c50
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0x18ab14c
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0xa19ca0
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0xa19e34
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0xa19f2c
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0xa579e8
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0xa57d6c
setvalue(so+py,4,0)
so=gg.getRangesList('libunity.so')[1].start
py=0x18ab134
setvalue(so+py,4,0)
gg.alert("防举报已开启")
end

function B()
KU = gg.choice({
"[🔘] 准备数据️ ✧ \n╰〖 自动飞天 〗",
" 自动飞天️ ✧ \n╰〖 控制上 〗",
" 自动飞天️ ✧ \n╰〖 控制下 〗",
"[🚡] 停留飞天️ ✧ \n╰〖 停留在当前高度 〗",
"[🚀] 快速上天️ ✧ \n╰〖 躲避外挂视线 〗}",
"[🚠] 浮游穿墙️ ✧ \n╰〖 不能下来自由穿墙 〗",
"[☑️] ️人物穿墙 ✧ \n╰〖 每局一开 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if KU == nil then HOME() else
if KU == 1 then KYG() end
if KU == 2 then UP() end
if KU == 3 then DOWN() end
if KU == 4 then STAY() end
if KU == 5 then FASTUP() end
if KU == 6 then FUYOU() end
if KU == 7 then WBP() end
end
HOMEDM = -1
end

function KYG()
gg.clearResults()
  gg.setRanges(gg.REGION_C_ALLOC, gg.REGION_ANONYMOUS)
  gg.searchNumber("-1090519040;1016003125;1045220557:41", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
  gg.searchNumber("-1090519040", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
  gg.getResults(10)
  gg.editAll("1040000000", gg.TYPE_DWORD)
  for SRD1_3_, SRD1_4_ in ipairs((gg.getResults(10))) do
    gg.getResults(10)[SRD1_3_].freeze = true
  end
  gg.addListItems((gg.getResults(10)))
  gg.clearResults()
end

function UP()
local t = gg.getListItems()
  do
    do
      for i, i in ipairs(t) do
        if i.flags == gg.TYPE_DWORD then
          i.value = "1040000000"
          i.freeze = true
          i.freezeType = gg.FREEZE_NORMAL
        end--XSanZ
      end--XSanZ
    end--XSanZ
  end--XSanZ
  gg.addListItems(t)
  t = nil
end--XSanZ

function DOWN()
local t = gg.getListItems()
  do
    do
      for i, i in ipairs(t) do
        if i.flags == gg.TYPE_DWORD then
          i.value = "-1099989877"
          i.freeze = true
          i.freezeType = gg.FREEZE_NORMAL
        end--XSanZ
      end--XSanZ
    end--XSanZ
  end--XSanZ
  gg.addListItems(t)
  t = nil
end--XSanZ

function STAY()
local t = MrTeamz.getListItems()
  do
    do
      for i, i in ipairs(t) do
        if i.flags == MrTeamz.TYPE_DWORD then
          i.value = "0"
          i.freeze = true
          i.freezeType = MrTeamz.FREEZE_NORMAL
        end--XSanZ
      end--XSanZ
    end--XSanZ
  end--XSanZ
  MrTeamz.addListItems(t)
  t = nil
end--XSanZ

function FASTUP()
local t = gg.getListItems()
  do
    do
      for i, i in ipairs(t) do
        if i.flags == gg.TYPE_DWORD then
          i.value = "1065000000"
          i.freeze = true
          i.freezeType = gg.FREEZE_NORMAL
        end--XSanZ
      end--XSanZ
    end--XSanZ
  end--XSanZ
  gg.addListItems(t)
  t = nil
end--XSanZ

function FUYOU()
local t = gg.getListItems()
for i, v in ipairs(t) do
	if v.flags == gg.TYPE_DWORD then
v.value = "2050000000"
v.freeze = true
v.freezeType = gg.FREEZE_NORMAL
	end
end
gg.addListItems(t)
t = nil
gg.toast("[🚠] 浮游穿墙️")
end

function WBP()
NAME = "人物穿墙"
gg.clearResults(850)
gg.setRanges(gg.REGION_C_ALLOC)
gg.searchNumber("1034147594;1051931443", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1034147594", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(850)
var = gg.getResultCount()
gg.editAll("2139000000", gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,叶仔有"..var.."个老婆")
end

function C()
RK = gg.multiChoice({
"[🎭] 内透功能️ ✧ \n╰〖 每局一开 〗",
"[⭕] 自瞄功能 ✧ \n╰〖 游戏内开 〗",
"[💯] 无后功能 ✧ \n╰〖 游戏内开 〗",
"[➕] 范围功能 ✧ \n╰〖 游戏内开 〗",
"[🔃] 切枪功能 ✧ \n╰〖 游戏内开 〗",
"[⚔️] 快刀功能️ ✧ \n╰〖 游戏内开 〗",
"[💀] 爆头功能 ✧ \n╰〖 游戏内开 〗",
"[🏘️] 穿墙功能 ✧ \n╰〖 游戏内开 〗",
"[🐍] 射速功能 ✧ \n╰〖 游戏内开 〗", 
"[🍌] 长名功能 ✧ \n╰〖 游戏内开 〗",
"[🦁] 准星聚点 ✧ \n╰〖 游戏内开 〗",
"[🔙] 返回主页 ✧ "
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if RK == nil then HOME() else
if RK[1] == true then MNXRAY() end
if RK[2] == true then MNAIMBOT() end
if RK[3] == true then MNNORECOIL() end
if RK[4] == true then MNMAGICBULLET() end
if RK[5] == true then MNFASTSWITCH() end
if RK[6] == true then MNFASTKNIFE() end
if RK[7] == true then MNHEADSHOT() end
if RK[8] == true then MNWALLBUG() end
if RK[9] == true then FASTSHOOT() end
if RK[10] == true then LONGNAME() end
if RK[11] == true then SMALL() end 
if RK[12] == true then HOME() end
end
HOMEDM = -1
end


function MNXRAY()
XR = gg.choice({
"[👤] 人物单透️ ✧ \n╰〖 仅骁龙处理器 〗",
"[👥] 人物双透️ ✧ \n╰〖 每局一开 〗",
"[🎭] 人物双透️ ✧ \n╰〖 Xs 〗",
"[🔍] 贴墙透视️ ✧ \n╰〖 每局一开 〗",
"[🔎] 贴墙透视 ✧ \n╰〖 Xs 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if XR == nil then C() else
if XR == 1 then XR1() end
if XR == 2 then XR2() end
if XR == 3 then XR3() end
if XR == 4 then XR4() end
if XR == 5 then XR5() end
end
HOMEDM = -1
end

function XR1()
qmnb = {
{["memory"] = 1048576},
{["name"] = "50%"},
{["value"] = 537333842, ["type"] = 4},
{["lv"] = 537333850, ["offset"] = -32, ["type"] = 4},
{["lv"] = 537333846, ["offset"] = -16, ["type"] = 4},
{["lv"] = 7, ["offset"] = 16, ["type"] = 4},
}
qmxg = {
{["value"] = 6, ["offset"] = 16, ["type"] = 4},
}
xqmnb(qmnb)
qmnb = {
{["memory"] = 1048576},
{["name"] = "100%"},
{["value"] = 1076887565, ["type"] = 4},
{["lv"] = 1078986752, ["offset"] = -16, ["type"] = 4},
{["lv"] = 1076889867, ["offset"] = -8, ["type"] = 4},
{["lv"] = 9, ["offset"] = 20, ["type"] = 4},
}
qmxg = {
{["value"] = 8, ["offset"] = 20, ["type"] = 4},
}
xqmnb(qmnb)
end

function XR2()
NAME = "人物双透"
gg.clearResults(3000)
gg.setRanges(bit32.bor(gg.REGION_C_ALLOC))
gg.searchNumber("65.793D;7.1746481e-43F;-3219128320Q:512", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("7.1746481e-43F;-3219128320Q", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
var = gg.getResultCount()
gg.editAll("-3146121216", gg.TYPE_QWORD)
gg.editAll("1.4160822e-39", gg.TYPE_FLOAT)
gg.alert(""..NAME.."开启成功,共修改"..var.."条数据")
end

function XR3()
--人物双透
qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "人物双透"},
{["value"] = 4368668252955669235, ["type"] = gg.TYPE_QWORD},
{["lv"] = 512, ["offset"] = 0x18, ["type"] = gg.TYPE_QWORD},
{["lv"] = -3219128320, ["offset"] = 0x48, ["type"] = gg.TYPE_QWORD},
}
qmxg = {
{["value"] = 1010550, ["offset"] = 0x18, ["type"] = gg.TYPE_QWORD},
{["value"] = -3146121216, ["offset"] = 0x48, ["type"] = gg.TYPE_QWORD},
}
xqmnb(qmnb)
end

function XR4()
NAME = "贴墙透视"
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC)
gg.searchNumber("1043878380;1148846080", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1043878380", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1076750000", gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function XR5()
 qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "贴墙透视"},
{["value"] = 1120403456, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1110704128, ["offset"] = 0x4, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1043878380, ["offset"] = 0x8, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1148846080, ["offset"] = 0xC, ["type"] = gg.TYPE_DWORD},
}
qmxg = {
{["value"] = 1075750000, ["offset"] = 0x8, ["type"] = gg.TYPE_DWORD},
}
xqmnb(qmnb)
end

function MNAIMBOT()
AIM = gg.choice({

"[⭕] 低调版自瞄 ✧ \n╰〖 游戏内开 〗",
"[⭕] 隔墙自瞄 ✧ \n╰〖 游戏内开 〗",
"[⭕] 自瞄头部 ✧ \n╰〖 游戏内开 〗",
"[⭕] 自瞄头部 ✧ \n╰〖 Xs 〗",
"[⭕] 自瞄锁敌 ✧ \n╰〖 游戏内开 〗",
"[⭕] 强锁自瞄 ✧ \n╰〖 游戏内开 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if AIM == nil then C() else
if AIM == 1 then AIM1() end
if AIM == 2 then AIM2() end
if AIM == 3 then AIM3() end
if AIM == 4 then AIM4() end
if AIM == 5 then AIM5() end
if AIM == 6 then AIM6() end
end
HOMEDM = -1
end

function AIM1()
NAME = "低调版自瞄"
gg.clearResults()
gg.searchNumber("1113927393;1073741824;416",gg.TYPE_DWORD,false,gg.SIGN_FUZZY_EQUAL,0,-1)
gg.searchNumber("1073741824",gg.TYPE_DWORD,false,gg.SIGN_FUZZY_EQUAL,0,-1)
gg.getResults(5000)
var = gg.getResultCount()
gg.editAll("1057000000",gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function AIM2()
gg.clearResults()
gg.setRanges(4)
gg.searchNumber("4;100;0.2", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("20", gg.TYPE_FLOAT)
gg.toast("隔牆自瞄 開啟成功")
end

function AIM3()
NAME = "自瞄头部"
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC)
gg.searchNumber("1,073,741,824;416;216", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1,073,741,824", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
var = gg.getResultCount()
gg.editAll("1,035,000,000", gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function AIM4()
qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "自瞄头部"},
{["value"] = 216, ["type"] = gg.TYPE_DWORD},
{["lv"] = 164, ["offset"] = 0x80, ["type"] = gg.TYPE_DWORD},
{["lv"] = 416, ["offset"] = 0x98, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1073741824, ["offset"] = 0xA8, ["type"] = gg.TYPE_DWORD},
}
qmxg = {
{["value"] = 1035000000, ["offset"] = 0xA8, ["type"] = gg.TYPE_DWORD},
}
xqmnb(qmnb)
end

function AIM5()
NAME = "自瞄锁敌"
gg.clearResults()
gg.setRanges(bit32.bor(gg.REGION_JAVA_HEAP, gg.REGION_C_HEAP, gg.REGION_C_ALLOC, gg.REGION_C_DATA, gg.REGION_C_BSS, gg.REGION_PPSSPP, gg.REGION_ANONYMOUS))
gg.searchNumber('1082130432;1120403456;1045220557', gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber('1120403456', gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
var = gg.getResultCount()
gg.editAll('0', gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function AIM6()
NAME = "强锁自瞄"
gg.clearResults()
gg.setRanges(4)
gg.searchNumber("0.01745329238F;57.295780181884766F", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("57.295780181884766", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
var = gg.getResultCount()
gg.editAll("0.8", gg.TYPE_FLOAT)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end



function MNNORECOIL()
MNNR = gg.choice({

"[💯] 枪械无后 ✧ \n╰〖 游戏内开 〗",
"[💯] 枪械无后 ✧ \n╰〖 Xs 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if MNNR == nil then C() else
if MNNR == 1 then NR1() end
if MNNR == 2 then NR2() end
end
HOMEDM = -1
end

function NR1()
NAME = "枪械无后"
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("0.1F~0.9F;900000~999762;100:113", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(50000)
var = gg.getResultCount()
gg.editAll("1.4012985e-45", gg.TYPE_FLOAT)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function NR2()
qmnb = {
{["memory"] = 4},
{["name"] = "枪械无后"},
{["value"] = 0.009999999776482582, ["type"] = 16},
{["lv"] = 1.0, ["offset"] = 8, ["type"] = 16},
{["lv"] = 0.009999999776482582, ["offset"] = 16, ["type"] = 16},
{["lv"] = 0.009999999776482582, ["offset"] = 48, ["type"] = 16},
}
qmxg = {
{["value"] = 0.1, ["offset"] = 8, ["type"] = 16},
}
xqmnb(qmnb)
end

function MNMAGICBULLET()
MNMB = gg.choice({

"[➕] 范围伤害小 ✧ \n╰〖 V1 〗",
"[➕] 范围伤害大 ✧ \n╰〖 V2 〗",
"[➕] 范围伤害自调 ✧ \n╰〖 V3 〗",
"[➕] 范围伤害 ✧ \n╰〖 叶仔自用 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if MNMB == nil then C() else
if MNMB == 1 then MB1() end
if MNMB == 2 then MB2() end
if MNMB == 3 then MB3() end
if MNMB == 4 then MB4() end
end
HOMEDM = -1
end

function MB1()
NAME = "范围伤害"
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("1061997773;1008981770;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1050000000", gg.TYPE_DWORD)
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("-1082130432;100;1036831949", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
var = gg.getResultCount()
gg.editAll("1050000000", gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function MB2()
NAME = "范围伤害"
gg.setRanges(gg.REGION_ANONYMOUS)
gg.clearResults()
gg.searchNumber("1008981770;100;1036831949",gg.TYPE_DWORD,false,gg.SIGN_FUZZY_EQUAL,0,-1)
gg.searchNumber("1008981770",gg.TYPE_DWORD,false,gg.SIGN_FUZZY_EQUAL,0,-1)
gg.getResults(10000)
gg.editAll("1060000000",gg.TYPE_DWORD)
gg.clearResults()
gg.searchNumber("-1082130432;100;1036831949",gg.TYPE_DWORD,false,gg.SIGN_FUZZY_EQUAL,0,-1)
gg.searchNumber("-1082130432",gg.TYPE_DWORD,false,gg.SIGN_FUZZY_EQUAL,0,-1)
gg.getResults(10000)
var = gg.getResultCount()
gg.editAll("1060000000",gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function MB3()
NAME = "范围伤害"
prompt = gg.prompt({
"┏━━━━━━━━━━━━━━━━━━━\n┣[➕] 范围伤害‖自调大小\n┣[🎥] YouTube: 叶仔YEZAI\n┗━━━━━━━━━━━━━━━━━━━\n [1050000000;1060000000]"
}, {
[1] = 1050000000
}, {
[1] = "number"
})
if not prompt then
return
end
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("-1082130432;100;1036831949", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
var = gg.getResultCount()
gg.editAll("" .. prompt[1] .. "", gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function MB4()
NAME = "范围伤害"
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("1008981770;100;1036831949", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(10000)
gg.editAll("1060000000", gg.TYPE_DWORD)
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("-1082130432;100;1036831949", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(10000)
var = gg.getResultCount()
gg.editAll("1060000000", gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function MNFASTSWITCH()
MNFSW = gg.choice({
"[🔃] 枪械秒切 ✧ \n╰〖 游戏内开 〗",
"[🔃] 枪械秒切 ✧ \n╰〖 Xs 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if MNFSW == nil then C() else
if MNFSW == 1 then FSW1() end
if MNFSW == 2 then FSW2() end
end
HOMEDM = -1
end

function FSW1()
NAME = "枪械秒切"
gg.setRanges(4)
gg.clearResults()
gg.searchNumber("1036831949;1065353216;1008981770:50", 4, false, 536870912, 0, -1)
gg.searchNumber("1065353216", 4, false, 536870912, 0, -1)
gg.getResults(4)
var = gg.getResultCount()
gg.editAll("1", 4)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function FSW2()
qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "快速切枪"},
{["value"] = 1061997773, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1065353216, ["offset"] = 0x8, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1008981770, ["offset"] = 0x10, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1036831949, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
qmxg = {
{["value"] = 1, ["offset"] = 0x8, ["type"] = gg.TYPE_DWORD},
}
xqmnb(qmnb)
end

function MNFASTKNIFE()
FK = gg.choice({
"[⚔️] 刀速增加 ✧ \n╰〖 游戏内开 〗",
"[⚔️] 刀速增加 ✧ \n╰〖 Xs 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if FK == nil then C() else
if FK == 1 then FK1() end
if FK == 2 then FK2() end
end
HOMEDM = -1
end

function FK1()
NAME = "刀速增加"
gg.clearResults()
gg.setRanges(bit32.bor(gg.REGION_JAVA_HEAP, gg.REGION_C_HEAP, gg.REGION_C_ALLOC, gg.REGION_C_DATA, gg.REGION_C_BSS, gg.REGION_PPSSPP, gg.REGION_ANONYMOUS))
gg.searchNumber("1008981770;1065353216;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1065353216", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
var = gg.getResultCount()
gg.editAll("1035000000", gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function FK2()
qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "刀速增加"},
{["value"] = 1119092736, ["type"] = gg.TYPE_DWORD},
{["lv"] = 584, ["offset"] = 0x50, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1065353216, ["offset"] = 0x70, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1008981770, ["offset"] = 0x78, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1069128089, ["offset"] = 0x84, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1036831949, ["offset"] = 0x88, ["type"] = gg.TYPE_DWORD},
}
qmxg = {
{["value"] = 1035000000, ["offset"] = 0x70, ["type"] = gg.TYPE_DWORD},
}
xqmnb(qmnb)
end

function MNHEADSHOT()
HS = gg.choice({

"[💀] 自动爆头 ✧ \n╰〖 V1 〗",
"[💀] 自动爆头 ✧ \n╰〖 V2 〗",
"[💀] 算法爆头 ✧ \n╰〖 游戏内开 〗",
"[💀] 刀具爆头 ✧ \n╰〖 游戏内开 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if HS == nil then RANK() else
if HS == 1 then HS1() end
if HS == 2 then HS2() end
if HS == 3 then HS3() end
if HS == 4 then HS4() end
end
HOMEDM = -1
end

function HS1()
NAME = "自动爆头"
gg.setRanges(gg.REGION_C_ALLOC)
gg.clearResults()
gg.searchNumber("1036831949;1047233823;-1114007142", gg.TYPE_DWORD,false,gg.SIGN_EQUAL,0, -1)
gg.searchNumber("1036831949", gg.TYPE_DWORD,false,gg.SIGN_EQUAL,0,-1)
gg.getResults(50)
var = gg.getResultCount()
gg.editAll("1,056,964,608",gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function HS2()
NAME = "自动爆头"
gg.clearResults()
gg.setRanges(4)
gg.searchNumber("-0.25;0.10000000149;0.23000000417;0.00499999989", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("0.1", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(1000)
var = gg.getResultCount()
gg.editAll("0.45", gg.TYPE_FLOAT)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function HS3()
NAME = "算法爆头"
gg.clearResults()
gg.setRanges(4)
gg.searchNumber("-0.25;0.10000000149;0.23000000417;0.00499999989", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("0.1", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(1000)
var = gg.getResultCount()
gg.editAll("0.25", gg.TYPE_FLOAT)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function HS4()
NAME = "刀具爆头"
gg.setRanges(bit32.bor(gg.REGION_JAVA_HEAP, gg.REGION_C_HEAP, gg.REGION_C_ALLOC, gg.REGION_C_DATA, gg.REGION_C_BSS, gg.REGION_PPSSPP, gg.REGION_ANONYMOUS))
gg.searchNumber("1113927393", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(300)
var = gg.getResultCount()
gg.editAll("1040353216", gg.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults()
end

function MNWALLBUG()
MWB = gg.choice({

"[🏘️] 人物穿墙 ✧ \n╰〖 每局一开 〗",
"[🏘️] 人物穿墙 ✧ \n╰〖 全局有效 〗",
"[🏘️] 人物穿墙 ✧ \n╰〖 Xa 〗",
"[🏘️] 人物穿墙 ✧ \n╰〖 Xs 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if MWB == nil then RANK() else
if MWB == 1 then WB1() end
if MWB == 2 then WB2() end
if MWB == 3 then WB3() end
if MWB == 4 then WB4() end
end
HOMEDM = -1
end

function WB1()
NAME = "人物穿墙"
gg.clearResults(850)
gg.setRanges(gg.REGION_C_ALLOC)
gg.searchNumber("1034147594;1051931443", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1034147594", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(850)
var = gg.getResultCount()
gg.editAll("2139000000", gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function WB2()
NAME = "人物穿墙"
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC)
gg.searchNumber("1045220557;1056964608;1028443341:41", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1056964608", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(1000)
var = gg.getResultCount()
gg.editAll("-1035220557", gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function WB3()
NAME = "人物穿墙"
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-1.54741583e26F;9.99999997e-7F;100.0F;-7.48689749e19F:21", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("9.99999997e-7", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
var = gg.getResultCount()
gg.editAll("999", gg.TYPE_FLOAT)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function WB4()
qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "人物穿墙"},
{["value"] = 1034147594, ["type"] = gg.TYPE_DWORD},
{["lv"] = 0, ["offset"] = 0x8, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1051931443, ["offset"] = 0x10, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1062836634, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
qmxg = {
{["value"] = 2139000000, ["offset"] = 0x0, ["type"] = gg.TYPE_DWORD},
}
xqmnb(qmnb)
end

function FASTSHOOT()
NAME = "射速"
MrTeamz.clearResults(3000)
  MrTeamz.setRanges(bit32.bor(MrTeamz.REGION_ANONYMOUS, MrTeamz.REGION_C_HEAP, MrTeamz.REGION_C_ALLOC))
  MrTeamz.searchNumber("1148846080;1060320051", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
  MrTeamz.getResults(5000)
  var = gg.getResultCount()
    MrTeamz.editAll("1000", MrTeamz.TYPE_DWORD)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function LONGNAME()
  gg.clearResults()
  gg.setRanges(32)
  gg.searchNumber("1F;8D", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
  gg.searchNumber("8", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
  gg.getResults(50000)
  gg.editAll("88", gg.TYPE_DWORD)
  gg.toast("16字超长名字代码，输入名字界面开")
  gg.clearResults()
end

function SMALL()
gg.setRanges(4)
local dataType = 16
local tb1 = {{10.0, 0}, {100.0, 32}, {1.0, 720}, }
local tb2 = {{0, 720}, }
SearchWrite(tb1, tb2, dataType)
end

function D()
WS = gg.choice({

"[☑️] 全枪墙射 ✧ \n╰〖 大厅内开 〗",
"[☑️] 狙击枪射 ✧ \n╰〖 大厅内开 〗",
"[☑️] 冲锋枪墙射 ✧ \n╰〖 大厅内开 〗",
"[☑️] 步枪墙射 ✧ \n╰〖 大厅内开 〗",
"[☑️] 机枪墙射 ✧ \n╰〖 大厅内开 〗",
"[☑️] 散弹墙射 ✧ \n╰〖 大厅内开 〗",
"[☑️] 手枪墙射 ✧ \n╰〖 大厅内开 〗",
"[☑️] 选择枪械 ✧ \n╰〖 大厅内开 〗",
"[🔙] 返回主页️ ✧ "
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if WS == nil then HOME() else
if WS == 1 then AWN() end
if WS == 2 then AWP() end
if WS == 3 then ALSMG() end
if WS == 4 then ALRFL() end
if WS == 5 then ALMG() end
if WS == 6 then ALSGN() end
if WS == 7 then ALPSTL() end
if WS == 8 then MNWEA() end
if WS == 9 then HOME() end
end
HOMEDM = -1
end

function AWN()
NAME = "全枪墙射"
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("0.1F~0.9F;900000~999762;1~10;100:113", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.refineNumber("1~10", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(50000)
var = gg.getResultCount()
gg.editAll("2139000000", gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function AWP()
NAME = "狙击墙射"
gg.setRanges(gg.REGION_ANONYMOUS)
gg.clearResults(5000)
gg.searchNumber('900127;5~9;-1082130432;1036831949;100', gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber('5~9', gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
var = gg.getResultCount()
gg.editAll('2144061856', gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function ALSMG()
NAME = "冲锋枪墙射"
gg.clearResults(5000)
gg.setRanges(gg.REGION_C_HEAP | gg.REGION_C_ALLOC | gg.REGION_ANONYMOUS)
gg.searchNumber("-1082130432;-1;900919;1~2;100:81", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1~2", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(9000)
var = gg.getResultCount()
gg.editAll("2144061856", gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function ALRFL()
NAME = "步枪墙射"
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("1008981770;-1;900762;4;100:81", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(9000)
var = gg.getResultCount()
gg.editAll("2144061856", gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function ALMG()
NAME = "机枪墙射"
gg.setRanges(gg.REGION_C_HEAP | gg.REGION_C_ALLOC | gg.REGION_ANONYMOUS)
gg.searchNumber("-1082130432;900762;3~5;100:81", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("3~5", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(9000)
gg.editAll("2144061856", gg.TYPE_DWORD)
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("-1082130432;901762;4;100:81", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(9000)
var = gg.getResultCount()
gg.editAll("2144061856", gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function ALSGN()
NAME = "散弹墙射"
gg.setRanges(gg.REGION_C_HEAP | gg.REGION_C_ALLOC | gg.REGION_ANONYMOUS)
gg.searchNumber("1053609165;1063675494;1008981770;-1;900012;1~2;100:93", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1~2", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(9000)
gg.editAll("2144061856", gg.TYPE_DWORD)
gg.clearResults()
gg.searchNumber("1008981770;900012;2;100:81", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("2", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(9000)
var = gg.getResultCount()
gg.editAll("2144061856", gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function ALPSTL()
NAME = "手枪墙射"
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("101114;-1082130432;2;100:273", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("2", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(500)
var = gg.getResultCount()
gg.editAll("2144061856", gg.TYPE_DWORD)
gg.clearResults(5000)
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
end

function MNWEA()
MWE = gg.choice({

"[☑️] 黑暗骑士 ✧ \n╰〖 游戏内开 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 游戏内开 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民槍戰全服外掛腳本\n┣[📆] 當前時間: %x\n┣[🕐] 當前時間: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if MWE == nil then WALLSHOT() else
if MWE == 1 then MNDARK() end
if MWE == 2 then MNDEATH() end
end
HOMEDM = -1
end

function MNDARK()
DRK = gg.multiChoice({
"[☑️] 黑暗骑士 ✧ \n╰〖 4 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 5 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 6 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 7 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 8 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 9 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 改 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 改36 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 改37 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 改38 〗",
"[☑️] 黑暗骑士 ✧ \n╰〖 改39 〗",
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if DRK == nil then WALLSHOT() else
if DRK[1] == true then DRAK1() end
if DRK[2] == true then DRAK2() end
if DRK[3] == true then DRAK3() end
if DRK[4] == true then DRAK4() end
if DRK[5] == true then DRAK5() end
if DRK[6] == true then DRAK6() end
if DRK[7] == true then DRAKM() end
if DRK[8] == true then DRAKm36() end
if DRK[9] == true then DRAKm37() end
if DRK[10] == true then DRAKm38() end
if DRK[11] == true then DRAKm39() end
end
HOMEDM = -1
end

function DRAK1()
gg.setRanges(gg.REGION_ANONYMOUS)
gg.searchNumber("403121;4;100;1008981770", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAK2()
gg.clearResults()
gg.searchNumber("403122;100;4;1008981770", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAK3()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("403123;1008981770;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAK4()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("403124D;1008981770D;4D;100D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770D;4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAK5()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("403125D;1008981770D;4D;100D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770D;4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAK6()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("403126D;1008981770D;4D;100D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770D;4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAKM()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("403127D;1008981770D;4D;100D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770D;4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAKm36()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("403128D;1008981770D;4D;100D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770D;4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAKm37()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("403129D;1008981770D;4D;100D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770D;4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAKm38()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("403130D;1008981770D;4D;100D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770D;4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function DRAKm39()
gg.clearResults()
gg.setRanges(gg.REGION_C_ALLOC)
gg.searchNumber("403,311D;4D;100D;1008981770D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1008981770D;4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(3000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "黑骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function MNDEATH()
D = gg.multiChoice({
"[☑️] 死亡骑士 ✧ \n╰〖 4 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 5 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 6 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 7 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 8 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 9 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 改 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 改36 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 改37 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 改38 〗",
"[☑️] 死亡骑士 ✧ \n╰〖 改39 〗",
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民槍戰全服外掛腳本\n┣[📆] 當前時間: %x\n┣[🕐] 當前時間: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if D == nil then MNWEA() else
if D[1] == true then death4() end
if D[2] == true then death5() end
if D[3] == true then death6() end
if D[4] == true then death7() end
if D[5] == true then death8() end
if D[6] == true then death9() end
if D[7] == true then deathM() end
if D[8] == true then deathm36() end
if D[9] == true then deathm37() end
if D[10] == true then deathm38() end
if D[11] == true then deathm39() end
end
HOMEDM = -1
end

function death4()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404121;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function death5()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404122;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function death6()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404123;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function death7()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404124;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function death8()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404125;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function death9()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404126;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function deathM()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404127;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function deathm36()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404128;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function deathm37()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404129;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function deathm38()
gg.clearResults()
gg.setRanges(gg.REGION_ANONYMOUS | gg.REGION_C_HEAP | gg.REGION_C_ALLOC)
gg.searchNumber("404130;-1082130432;4;100", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432;4", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function deathm39()
gg.clearResults()
gg.setRanges(gg.REGION_JAVA_HEAP | gg.REGION_C_HEAP | gg.REGION_C_ALLOC | gg.REGION_C_DATA | gg.REGION_C_BSS | gg.REGION_PPSSPP | gg.REGION_ANONYMOUS)
gg.searchNumber("404231D;4D;100D;-1082130432D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432D;4D", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("1063000000", gg.TYPE_DWORD)
var = gg.getResultCount()
NAME = "死骑墙射"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end



function E()
VE = MrTeamz.multiChoice({
"「🐙」挑战子弹追踪・人机",
"「👹」地狱子弹追踪・人机",
"「👽」争霸子弹追踪・人机",
"「🐉」降龙子弹追踪・人机",
"「👺」俱乐部定怪・人机",
"「👺」俱乐部定怪・游戏",
"「😈」百鬼夜行怪物不动・游戏",
"「🐉」降龙怪物不动・飞机",
"「💉」怪物变傻・大厅",
"「🔙」返回主页"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if VE == nil then HOME()else
if VE[1] == true then HARD() end
if VE[2] == true then HELL() end
if VE[3] == true then TC() end
if VE[4] == true then DS() end
if VE[5] == true then BOSSD() end
if VE[6] == true then BOSSDM() end
if VE[7] == true then BAIGUI() end
if VE[8] == true then XIANGD() end
if VE[9] == true then BODO() end
if VE[10] == true then HOME() end
end
HOMEDM = -1
end

function HARD()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3010;360;1058088681", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("1058088681", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("2139000000", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("20%...")
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3011;160;3;1059776403", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3;1059776403", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("2139000000", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("30%...")
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3014;120;1065353216", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("1065353216", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("2139000000", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("40%...")
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3010~3011;360", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3010~3011", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5101", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("50%...")
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3001~3033;120 ", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3001~3033", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("60%...")
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3022;180 ", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3022", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("70%...")
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("1038442562", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("1028442562", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("85%...")
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("1054951342;1061997773", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("1", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("95%...")
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3003", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("༆ 开启成功 ༄")
end

function HELL()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.clearResults()
MrTeamz.searchNumber("3001~3024;120", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3001~3024", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.searchNumber("5201~5205;120", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("5201~5205", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.searchNumber("5102~5103;360", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("5102~5103", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.searchNumber("3022;180", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3022", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("༆ 开启成功 ༄")
end

function TC()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3001~3033;120", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3001~3033", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(850)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("40%...")
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("5201~5205", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("5201~5205", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(850)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("60%...")
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC)
MrTeamz.searchNumber("1008981770;184;92", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("1008981770", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(10)
MrTeamz.editAll("1036831949", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("80%...")
MrTeamz.toast("༆ 开启成功 ༄")
end

function DS()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3010;360;1058088681", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("1058088681", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("2139000000", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("20%...")
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3011;160;3;1059776403", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3;1059766403", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("2139000000", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("40%...")
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3014;120;1065353216", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("1065353216", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("2139000000", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.clearResults(5000)
MrTeamz.toast("60%...")
MrTeamz.searchNumber("3001~3033;120", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3001~3033", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults(5000)
MrTeamz.toast("70%...")
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.clearResults(5000)
MrTeamz.searchNumber("3101;120", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3101", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults(5000)
MrTeamz.toast("80%...")
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("5201~5209;120", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("5201~5209", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults(5000)
MrTeamz.toast("90%...")
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3022;180 ", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3022", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults(5000)
MrTeamz.toast("༆ 开启成功 ༄")
end

function BOSSD()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("5208~5209", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("5208~5209", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.toast("20%")
MrTeamz.getResults(850)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3001~3033;180", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("3001~3033", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.toast("40")
MrTeamz.getResults(850)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3035", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.toast("50")
MrTeamz.getResults(850)
MrTeamz.editAll("112001", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("3034", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.toast("60%")
MrTeamz.getResults(850)
MrTeamz.editAll("112001", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("5206;120;2", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("2", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.toast("85%")
MrTeamz.getResults(5000)
MrTeamz.editAll("2139000000", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("5201~5206;120", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("5201~5206", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(850)
MrTeamz.editAll("5002", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
MrTeamz.toast("༆ 开启成功 ༄")
end

function BOSSDM()
MrTeamz.clearResults()
MrTeamz.setRanges(4)
MrTeamz.searchNumber("9.7e-322E;0.1;0.2", MrTeamz.TYPE_FLOAT, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("0.1", MrTeamz.TYPE_FLOAT, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(100)
MrTeamz.editAll("8555", MrTeamz.TYPE_FLOAT)
MrTeamz.toast("༆ 开启成功 ༄")
MrTeamz.clearResults()
end

function BAIGUI()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC)
MrTeamz.searchNumber("2524D;0.10000000149", MrTeamz.TYPE_FLOAT, false, nil, 0, -1)
MrTeamz.searchNumber("0.10000000149", MrTeamz.TYPE_FLOAT, false, nil, 0, -1)
MrTeamz.getResults(30)
MrTeamz.editAll("999,", MrTeamz.TYPE_FLOAT)
MrTeamz.toast("༆ 开启成功 ༄")
end

function XIANGD()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC)
MrTeamz.searchNumber("69764D;0.89999997616", MrTeamz.TYPE_FLOAT, false, nil, 0, -1)
MrTeamz.searchNumber("0.89999997616", MrTeamz.TYPE_FLOAT, false, nil, 0, -1)
MrTeamz.getResults(30)
MrTeamz.editAll("999", MrTeamz.TYPE_FLOAT)
MrTeamz.toast("༆ 开启成功 ༄")
end



function F()
MNC = gg.multiChoice({

"[🏞️] 粉色身体 ✧ \n╰〖 游戏内开 〗",
"[🏜]️ 黄色身体 ✧ \n╰〖 游戏内开 〗",
"[🏖]️ 红色身体 ✧ \n╰〖 游戏内开 〗",
"[🏝️] 绿色身体 ✧ \n╰〖 游戏内开 〗",
"[🏙️] 随机身体 ✧ \n╰〖 游戏内开 〗",
"[🌁] 白色身体 ✧ \n╰〖 游戏内开 〗",
"[🌅] 白色枪械 ✧ \n╰〖 游戏内开 〗",
"[🌉] 黑色枪械 ✧ \n╰〖 游戏内开 〗",
"[🌃] 黑色天空 ✧ \n╰〖 游戏内开 〗",
"[🌌] 黑色地图 ✧ \n╰〖 游戏内开 〗",
"[⬛] 黑色身体 ✧ \n╰〖 游戏内开 〗",
"[💡] 人物发亮 ✧ \n╰〖 游戏内开 〗",
"[🔙] 返回主页 ✧ "
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民槍戰全服外掛腳本\n┣[📆] 當前時間: %x\n┣[🕐] 當前時間: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if MNC == nil then HOME() else
if MNC[1] == true then PINK() end
if MNC[2] == true then YELLOW() end
if MNC[3] == true then RED() end
if MNC[4] == true then GREEN() end
if MNC[5] == true then RAMDOM() end
if MNC[6] == true then WHITEB() end
if MNC[7] == true then WHITEG() end
if MNC[8] == true then BLACKG() end
if MNC[9] == true then BLACKSKY() end
if MNC[10] == true then BLACKMAP() end
if MNC[11] == true then BLACK() end
if MNC[12] == true then LIGHT() end
if MNC[13] == true then HOME() end
end
HOMEDM = -1
end

function PINK()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC)
MrTeamz.searchNumber("259998699", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(10000)
MrTeamz.editAll("1259998699", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end

function GREEN()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC, MrTeamz.REGION_ANONYMOUS, MrTeamz.REGION_BAD)
MrTeamz.clearResults(500)
MrTeamz.searchNumber("537301028", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(500)
MrTeamz.editAll("1007700029", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end

function YELLOW()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_VIDEO)
MrTeamz.searchNumber("671088640;671285249:9" , MrTeamz.TYPE_DWORD)
MrTeamz.searchNumber("671285249" , MrTeamz.TYPE_DWORD)
MrTeamz.getResults(3000)
MrTeamz.editAll("2130935614" , MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end


function RED()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC | MrTeamz.REGION_ANONYMOUS | MrTeamz.REGION_BAD)
MrTeamz.searchNumber("805325056", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(500)
MrTeamz.editAll("1007681770", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end

function RANDOM()
MrTeamz.clearResults()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC | MrTeamz.REGION_ANONYMOUS | MrTeamz.REGION_BAD)
MrTeamz.searchNumber("270532608;537301028", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("1040532608", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end

function WHITEB()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC)
MrTeamz.searchNumber("79;1061997773", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.refineNumber("1061997773", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(10000, nil, nil, nil, nil, nil, nil, nil, nil)
MrTeamz.editAll("2061997773", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end

function WHITEG()
MrTeamz.clearResults()
MrTeamz.setRanges(bit32.bor(MrTeamz.REGION_C_ALLOC, MrTeamz.REGION_ANONYMOUS, MrTeamz.REGION_BAD))
MrTeamz.clearResults(500)
MrTeamz.searchNumber("327689", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(300)
MrTeamz.editAll("0", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end
  
function BLACKG()
MrTeamz.clearResults()
MrTeamz.setRanges(bit32.bor(MrTeamz.REGION_C_ALLOC, MrTeamz.REGION_ANONYMOUS, MrTeamz.REGION_BAD))
MrTeamz.clearResults(500)
MrTeamz.searchNumber("327689", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(300)
MrTeamz.editAll("9999", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end
  
function BLACKMAP()
BM = MrTeamz.choice({
"「🌌」黑色地圖・開啟", 
"「🌌」黑色地圖・關閉"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if BM == nil then MNCOLOR() else
if BM == 1 then BMON() end
if BM== 2 then BMOF() end
end
HOMEDM = -1
end

function BMON()
MrTeamz.clearResults()
MrTeamz.setRanges(bit32.bor(MrTeamz.REGION_JAVA_HEAP, MrTeamz.REGION_C_HEAP, MrTeamz.REGION_C_ALLOC, MrTeamz.REGION_C_DATA, MrTeamz.REGION_C_BSS, MrTeamz.REGION_PPSSPP, MrTeamz.REGION_ANONYMOUS))
MrTeamz.clearResults(500)
MrTeamz.searchNumber("-50384417", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(300)
MrTeamz.editAll("-50384410", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "地圖黑色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end

function BMOF()
MrTeamz.clearResults()
MrTeamz.setRanges(bit32.bor(MrTeamz.REGION_JAVA_HEAP, MrTeamz.REGION_C_HEAP, MrTeamz.REGION_C_ALLOC, MrTeamz.REGION_C_DATA, MrTeamz.REGION_C_BSS, MrTeamz.REGION_PPSSPP, MrTeamz.REGION_ANONYMOUS))
MrTeamz.clearResults(500)
MrTeamz.searchNumber("-50384410", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(300)
MrTeamz.editAll("-50384417", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "地圖黑色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end

function BLACKSKY()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS | MrTeamz.REGION_C_HEAP | MrTeamz.REGION_C_ALLOC)
MrTeamz.searchNumber("1008981770;1148846080;100", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.refineNumber("1148846080", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
revert = MrTeamz.getResults(30)
MrTeamz.editAll("1111111111", MrTeamz.TYPE_DWORD)
var = MrTeamz.getResultCount()
NAME = "黑色天空"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end

function LIGHT()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC)
MrTeamz.searchNumber("0.8;0.6;2", MrTeamz.TYPE_FLOAT, false, MrTeamz.SIGN_EQUAL, 0, -1, 0)
MrTeamz.refineNumber("0.8", MrTeamz.TYPE_FLOAT, false, MrTeamz.SIGN_EQUAL, 0, -1, 0)
MrTeamz.getResults(100, nil, nil, nil, nil, nil, nil, nil, nil)
MrTeamz.editAll("12", MrTeamz.TYPE_FLOAT)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end

function BLACK()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC)
MrTeamz.searchNumber("0.8;0.6;2", MrTeamz.TYPE_FLOAT, false, MrTeamz.SIGN_EQUAL, 0, -1, 0)
MrTeamz.refineNumber("0.8", MrTeamz.TYPE_FLOAT, false, MrTeamz.SIGN_EQUAL, 0, -1, 0)
MrTeamz.getResults(100, nil, nil, nil, nil, nil, nil, nil, nil)
MrTeamz.editAll("-99999", MrTeamz.TYPE_FLOAT)
var = MrTeamz.getResultCount()
NAME = "人物上色"
MrTeamz.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
MrTeamz.clearResults(5000)
end



function G()
ZJ2 = gg.choice({

"[🚟] 飞天遁地 ✧ 🇹🇼\n╰〖 Ca 〗",
"[🚟] 飞天遁地️ ✧ 🇲🇾\n╰〖 Xs 〗"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if ZJ2 == nil then HOME() else
if ZJ2 == 1 then FU1() end
if ZJ2 == 2 then FU2() end
end
HOMEDM = -1
end

function FU1()
NY = gg.choice({
   "[♂️] 男角 ✧ 🇹🇼\n╰〖 游戏内开 〗",
   "[♀️] 女角 ✧ 🇹🇼\n╰〖 游戏内开 〗",
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民槍戰全服外掛腳本\n┣[📆] 當前時間: %x\n┣[🕐] 當前時間: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if NY == nil then G()else
if NY == 1 then FUBOY() end
if NY == 2 then FUGIRL() end
end
HOMEDM = -1
end

function FUBOY()
BOY = gg.choice({
    "[🚁] 飞天 ✧ 🇹🇼\n╰〖 游戏内开 〗",
    "[🛳️] 遁地 ✧ 🇹🇼\n╰〖 游戏内开 〗",
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民槍戰全服外掛腳本\n┣[📆] 當前時間: %x\n┣[🕐] 當前時間: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if BOY == nil then FU1()else
if BOY == 1 then ABC1() end
if BOY == 2 then ABC2() end
end
HOMEDM = -1
end

function ABC1()
gg.clearResults(3000)
gg.setRanges(bit32.bor(gg.REGION_JAVA_HEAP,gg.REGION_C_HEAP,gg.REGION_C_ALLOC,gg.REGION_C_DATA,gg.REGION_C_BSS,gg.REGION_PPSSPP,gg.REGION_ANONYMOUS))
gg.searchNumber("1034147594;1051931443;1062836634", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1062836634", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
prompt = gg.prompt({"┏━━━━━━━━━━━━━━━━━━━\n┣[🚟] 飞天高度\n┣[🎥] 叶仔YEZAI\n┗━━━━━━━━━━━━━━━━━━━[-1057836634;-1000836634]"},{[1] = -1040836634},{[1] = "number"})
repeat
repeat
do break end
do break end
return
until true
until true
gg.getResults(5000)
gg.editAll(prompt[1], gg.TYPE_DWORD)
NAME = "男角飞天"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function ABC2()
gg.clearResults(3000)
gg.setRanges(bit32.bor(gg.REGION_JAVA_HEAP,gg.REGION_C_HEAP,gg.REGION_C_ALLOC,gg.REGION_C_DATA,gg.REGION_C_BSS,gg.REGION_PPSSPP,gg.REGION_ANONYMOUS))
gg.searchNumber("1034147594;1051931443;1062836634", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1062836634", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
prompt = gg.prompt({"┏━━━━━━━━━━━━━━━━━━━\n┣[🚟] 遁地高度\n┣[🎥] 叶仔YEZAI\n┗━━━━━━━━━━━━━━━━━━━[1080836634;1122000000]"},{[1] = 1095836634},{[1] = "number"})
repeat
repeat
do break end
do break end
return
until true
until true
gg.getResults(5000)
gg.editAll(prompt[1], gg.TYPE_DWORD)
NAME = "男角遁地"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function FUGIRL()
GIRL = gg.choice({
    "[🚁] 飞天 ✧ 🇲🇾\n╰〖 游戏内开 〗",
    "[🛳️] 遁地 ✧ 🇲🇾\n╰〖 游戏内开 〗",
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if GIRL == nil then FU1()else
if GIRL == 1 then ABC3() end
if GIRL == 2 then ABC4() end
end
HOMEDM = -1
end

function ABC3()
gg.clearResults(3000)
gg.setRanges(bit32.bor(gg.REGION_JAVA_HEAP,gg.REGION_C_HEAP,gg.REGION_C_ALLOC,gg.REGION_C_DATA,gg.REGION_C_BSS,gg.REGION_PPSSPP,gg.REGION_ANONYMOUS))
gg.searchNumber("1034147594;1051931443;1062417203", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1062417203", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
prompt = gg.prompt({"┏━━━━━━━━━━━━━━━━━━━\n┣[🚟] 飞天高度\n┣[🎥] 叶仔YEZAI\n┗━━━━━━━━━━━━━━━━━━━[-1057836634;-1000836634]"},{[1] = -1040836634},{[1] = "number"})
repeat
repeat
do break end
do break end
return
until true
until true
gg.getResults(5000)
gg.editAll(prompt[1], gg.TYPE_DWORD)
NAME = "女角飞天"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function ABC4()
gg.clearResults(3000)
gg.setRanges(bit32.bor(gg.REGION_JAVA_HEAP,gg.REGION_C_HEAP,gg.REGION_C_ALLOC,gg.REGION_C_DATA,gg.REGION_C_BSS,gg.REGION_PPSSPP,gg.REGION_ANONYMOUS))
gg.searchNumber("1034147594;1051931443;1062417203", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("1062417203", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
prompt = gg.prompt({"┏━━━━━━━━━━━━━━━━━━━\n┣[🚟] 遁地高度\n┣[🎥] 叶仔YEZAI\n┗━━━━━━━━━━━━━━━━━━━[1080836634;1122000000]"},{[1] = 1095836634},{[1] = "number"})
repeat
repeat
do break end
do break end
return
until true
until true
gg.getResults(5000)
gg.editAll(prompt[1], gg.TYPE_DWORD)
NAME = "女角遁地"
gg.toast(""..NAME.."开启成功,共修改"..var.."条数据")
gg.clearResults(5000)
end

function FU2()
NWA = gg.choice({
"[🚟] 男角飞天 ✧ 🇲🇾\n╰〖 游戏内开 〗",
"[🚟] 女角飞天 ✧ 🇲🇾\n╰〖 游戏内开 〗",
"[🚟] 男角遁地 ✧ 🇲🇾\n╰〖 游戏内开 〗",
"[🚟] 女角遁地 ✧ 🇲🇾\n╰〖 游戏内开 〗",
"[🔙] 返回主页 ✧ 🇲🇾"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[🌐] 全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if NWA == true then G() else
if NWA == 1 then FLYCO() end
if NWA == 2 then FLYCE() end
if NWA == 3 then UGCO() end
if NWA == 4 then UCCE() end
if NWA == 5 then FLYUG() end
end
HOMEDM = -1
end

function FLYCO()
qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "男角飞天"},
{["value"] = 1034147594, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1051931443, ["offset"] = 0x10, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1062836634, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
qmxg = {
{["value"] = -1040000000, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
xqmnb(qmnb)
end
  
function FLYCE()
qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "女角飞天"},
{["value"] = 1034147594, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1051931443, ["offset"] = 0x10, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1062417203, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
qmxg = {
{["value"] = -1040000000, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
xqmnb(qmnb)
end

function UGCO()
qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "男角遁地"},
{["value"] = 1034147594, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1051931443, ["offset"] = 0x10, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1062836634, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
qmxg = {
{["value"] = 1080000000, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
xqmnb(qmnb)
end

function UCCE()
qmnb = {
{["memory"] = gg.REGION_C_ALLOC},
{["name"] = "女角遁地"},
{["value"] = 1034147594, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1051931443, ["offset"] = 0x10, ["type"] = gg.TYPE_DWORD},
{["lv"] = 1062417203, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
qmxg = {
{["value"] = 1080000000, ["offset"] = 0x18, ["type"] = gg.TYPE_DWORD},
}
xqmnb(qmnb)
end

function H()
MNOH = MrTeamz.choice({

" 男角遁地・游戏",
" 女角遁地・游戏",
" 子弹追踪・狙击",
" 子弹追踪・步枪",
" 子弹追踪・散弹黑騎",
" 浮游穿墙・游戏",
"「🔙」返回主页"
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣全民枪战美服脚本\n┣[📆] 当前时间: %x\n┣[🕐] 当前时间: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if MNOH == nil then HOME() else
if MNOH == 1 then NANDUN() end 
if MNOH == 2 then NVDUN() end
if MNOH == 3 then OHSNIPER() end
if MNOH == 4 then OHSG() end
if MNOH == 5 then OHSMG() end
if MNOH == 6 then XUYONG() end
if MNOH == 7 then HOME() end
end
HOMEDM = -1
end

function NANDUN()
qmnb = {
{["memory"] = MrTeamz.REGION_C_ALLOC},
{["name"] = "男角遁地"},
{["value"] = 1034147594, ["type"] = MrTeamz.TYPE_DWORD},
{["lv"] = 1051931443, ["offset"] = 0x10, ["type"] = MrTeamz.TYPE_DWORD},
{["lv"] = 1062836634, ["offset"] = 0x18, ["type"] = MrTeamz.TYPE_DWORD},
}
qmxg = {
{["value"] = 1133836634, ["offset"] = 0x18, ["type"] = MrTeamz.TYPE_DWORD},
}
xqmnb(qmnb)
end

function NVDUN()
qmnb = {
{["memory"] = MrTeamz.REGION_C_ALLOC},
{["name"] = "女角遁地"},
{["value"] = 1034147594, ["type"] = MrTeamz.TYPE_DWORD},
{["lv"] = 1051931443, ["offset"] = 0x10, ["type"] = MrTeamz.TYPE_DWORD},
{["lv"] = 1062417203, ["offset"] = 0x18, ["type"] = MrTeamz.TYPE_DWORD},
}
qmxg = {
{["value"] = 1133836634, ["offset"] = 0x18, ["type"] = MrTeamz.TYPE_DWORD},
}
xqmnb(qmnb)
end

function OHSNIPER()
gg.clearResults()
gg.setRanges(gg.REGION_C_HEAP | gg.REGION_C_ALLOC | gg.REGION_ANONYMOUS)
gg.searchNumber("-1082130432;1013276738;150", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("-1082130432", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(850)
gg.editAll("2139666666", gg.TYPE_DWORD)
gg.toast("༆ 开启成功 ༄")
gg.clearResults()
end

function OHSG()
gg.setRanges(gg.REGION_C_HEAP | gg.REGION_C_ALLOC | gg.REGION_ANONYMOUS)
gg.searchNumber("1036831949;100;-1082130432", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("100;-1082130432", gg.TYPE_DWORD, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(5000)
gg.editAll("2139000000", gg.TYPE_DWORD)
gg.clearResults()
MrTeamz.toast("༆ 开启成功 ༄")
end

function OHSMG()
MrTeamz.setRanges(MrTeamz.REGION_ANONYMOUS)
MrTeamz.searchNumber("1008981770;1061997773;100", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.searchNumber("1008981770;100", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.getResults(5000)
MrTeamz.editAll("2,139,000,000", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults(5000)
MrTeamz.clearResults(5000)
MrTeamz.toast("༆ 开启成功 ༄")
end

function XUYONG()
MrTeamz.setRanges(MrTeamz.REGION_C_ALLOC)
MrTeamz.clearResults()
MrTeamz.searchNumber("1008981770;1061997773;-1090519040", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
MrTeamz.refineNumber("-1090519040", MrTeamz.TYPE_DWORD, false, MrTeamz.SIGN_EQUAL, 0, -1)
revert = MrTeamz.getResults(100, nil, nil, nil, nil, nil, nil, nil, nil)
var = MrTeamz.getResultCount()
MrTeamz.editAll("2050000000", MrTeamz.TYPE_DWORD)
MrTeamz.clearResults()
end

function I()
ZJX = gg.choice({
"「☑️」開啟菜單",
"「❎」關閉菜單",
"「🔙」返回主頁",
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[😈] 全民槍戰美服腳本\n┣[📆] 當前時間: %x\n┣[🕐] 當前時間: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if ZJX == nil then HOME() else
if ZJX == 1 then MNON() end
if ZJX == 2 then MNOF() end
if ZJX == 3 then HOME() end
end
HOMEDM = -1
end

function MNON()
ON = gg.choice({
"「♈」人物穿牆",
"「♉」子彈穿牆",
"「♊」身體範圍",
"「♋」頭部範圍",
"「♌」跳躍爬牆",
"「♍」子彈全穿",
"「♎」槍械無後",
"「♏」原地刀人",
"「♐」音量變大",
"「♑」視角變大",
"「🔙」返回主頁",
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[😈] 全民槍戰美服腳本\n┣[📆] 當前時間: %x\n┣[🕐] 當前時間: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if ON == nil then MNXA() else
if ON == 1 then WBON() end
if ON == 2 then WSON() end
if ON == 3 then MBON() end
if ON == 4 then HSON() end
if ON == 5 then PAON() end
if ON == 6 then WSAON() end
if ON == 7 then NRON() end
if ON == 8 then HKON() end
if ON == 9 then BSON() end
if ON == 10 then SJON() end
if ON == 11 then MNXA() end
end
HOMEDM = -1
end

function WBON()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-1.54741583e26F;9.99999997e-7F;100.0F;-7.48689749e19F:21", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("9.99999997e-7", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("999", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function WSON()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-7.91031686e27F;-1.54741518e26F;9.99999997e-7F;-1.30904183e25F:17", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("9.99999997e-7", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("999", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function MBON()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("1.36458613e-38F;0.70710676908F;1.36458276e-38F;1.36455586e-38F", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("0.70710676908", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("5", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function HSON()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("1,477,255,424.0F;1,477,255,424.0F;1,476,731,136.0F;0.00001F;6.16304268e-33F", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("0.00001", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("0.23", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function PAON()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("0.0001F;4.9850323e-315E", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("4.9850323e-315", gg.TYPE_DOUBLE, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("999", gg.TYPE_DOUBLE)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function WSAON()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-1.54741583e26F;9.99999997e-7F;100.0F;-7.48689749e19F:21", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("9.99999997e-7", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("999", gg.TYPE_FLOAT)
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-7.91031686e27F;-1.54741518e26F;9.99999997e-7F;-1.30904183e25F:17", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("9.99999997e-7", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("999", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function NRON()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("1.2280907e-38F;57.29577636719F;-1.3092761e25F;-5.477952e24F", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("57.29577636719", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("0", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function HKON()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-7.15911681e24F;9.99999987e14F;0.00001F;-1.30927611e25F", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("0.00001", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("999", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function BSON()
gg.clearResults()
gg.searchNumber("2", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
revert = gg.getResults(100, nil, nil, nil, nil, nil, nil, nil, nil)
gg.editAll("1011", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function SJON()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("360;-7.16042653e24;3.14159274101;-9.91623292e27", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("360", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("140", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function MNOF()
OF = gg.choice({
" 人物穿牆 ",
" 子彈穿牆 ",
" 身體範圍 ",
" 頭部範圍 ",
" 跳躍爬牆 ",
" 子彈全穿 ",
" 槍械無後 ",
" 原地刀人 ",
" 音量變大 ",
" 視角變大 ",
"「🔙」返回主頁",
}, nil,(os.date("┏━━━━━━━━━━━━━━━━━━━\n┣[😈] 全民槍戰美服腳本\n┣[📆] 當前時間: %x\n┣[🕐] 當前時間: %X\n┗━━━━━━━━━━━━━━━━━━━")))
if OF == nil then MNXA() else
if OF == 1 then WBOF() end
if OF == 2 then WSOF() end
if OF == 3 then MBOF() end
if OF == 4 then HSOF() end
if OF == 5 then PAOF() end
if OF == 6 then WSAOF() end
if OF == 7 then NROF() end
if OF == 8 then HKOF() end
if OF == 9 then BSOF() end
if OF == 10 then SJOF() end
if OF == 11 then MNXA() end
end
HOMEDM = -1
end

function WBOF()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-1.54741583e26F;999F;100.0F;-7.48689749e19F:21", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("999", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("9.99999997e-7", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function WSOF()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-7.91031686e27F;-1.54741518e26F;999F;-1.30904183e25F:17", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("999", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("9.99999997e-7", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function MBOF()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("1.36458613e-38F;5F;1.36458276e-38F;1.36455586e-38F", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("5", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("0.70710676908", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function HSOF()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("1,477,255,424.0F;1,477,255,424.0F;1,476,731,136.0F;0.23F;6.16304268e-33F", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("0.23", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("0.00001", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function PAOF()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("0.0001F;999E", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("999", gg.TYPE_DOUBLE, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("4.9850323e-315", gg.TYPE_DOUBLE)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function WSAOF()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-1.54741583e26F;999F;100.0F;-7.48689749e19F:21", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("999", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("9.99999997e-7", gg.TYPE_FLOAT)
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-7.91031686e27F;-1.54741518e26F;999F;-1.30904183e25F:17", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("999", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("9.99999997e-7", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function NROF()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("1.2280907e-38F;0F;-1.3092761e25F;-5.477952e24F", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("0", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("57.29577636719 ", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function HKOF()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("-7.15911681e24F;9.99999987e14F;999F;-1.30927611e25F", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("999", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("0.00001", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function BSOF()
gg.searchNumber("1011", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
revert = gg.getResults(5000, nil, nil, nil, nil, nil, nil, nil, nil)
gg.editAll("2", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function SJOF()
gg.clearResults()
gg.setRanges(16384)
gg.searchNumber("140;-7.16042653e24;3.14159274101;-9.91623292e27", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.searchNumber("140", gg.TYPE_FLOAT, false, gg.SIGN_EQUAL, 0, -1)
gg.getResults(100)
gg.editAll("360", gg.TYPE_FLOAT)
var = gg.getResultCount()
NAME = "XA功能"
gg.toast(""..NAME.."開啟成功,共修改"..var.."條數據")
gg.clearResults(5000)
end

function CLOSE()
print(os.date("📆時間 - %A - %B - %d - %Y / 時間 :%H:%M:%S %Z\n🔴YouTube 叶仔 \n叶仔二改辅助 \n⏩請勿转卖此免费脚本"))
gg.copyText("https://youtube.com/channel/UCPn30qAX5_RudbNxoPpU4hA")
gg.toast("已复制作者频道链接")
os.exit()
end

while true do
  if gg.isVisible(true) then
    HOMEDM = 1
  gg.setVisible(false)
  end
  if HOMEDM == 1 then
    HOME()
  end
end
