# -*- coding: utf-8 -*-
# this file is released under public domain and you can use without limitations

#########################################################################
## This is a sample controller
## - index is the default action of any application
## - user is required for authentication and authorization
## - download is for downloading files uploaded in the db (does streaming)
#########################################################################
L = []
TL = []
AL = []
TCL = {}
ACL = {}

ENTITY_DICT ={'ABBREVIATION':'blueviolet', 'FAMILY':'darkblue', 'FORMULA':'green', 'IDENTIFIER':'orange', 'MULTIPLE':'pink', 'SYSTEMATIC':'red','TRIVIAL':'brown'}


def index():
    response.flash = T("Welcome to CNER Demonstration")
    return dict()

def getSpan(E):
	return '<span style="color:' + ENTITY_DICT[E[5]] + ';font-weight:bold">' + E[4] + '</span>'


def process():
    response.flash = T("Patent title and abstract annotated")
    x = request.vars.patentnumber
    y = request.vars.patenttitle
    z = request.vars.patentabstract
    a = request.vars.annotations
    l = a.split('\r\n')

    for b in l:
        L.append(b.split('|'))
    for i in L:
        pos = i[1]
        if pos == 'T':
            TL.append(i)
        else:
            AL.append(i)

    for j in TL:
        replacement = getSpan(j)
        original    = j[4]
	if TCL.has_key(j[4]):
		TCL[j[4]] += 1
		pass
	else:
		y = y.replace(original, replacement)
		TCL[j[4]] = 1

    for k in AL:
        replacement = getSpan(k)
        original    = k[4]
	if ACL.has_key(k[4]):
		ACL[k[4]] += 1
		pass
	else:
		z = z.replace(original, replacement)
		ACL[k[4]] = 1
    y = '<p>' + y + '</p>'
    z = '<p>' + z + '</p>'

    return dict(x=x,y=y,z=z)
