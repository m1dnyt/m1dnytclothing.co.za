# m1dnytclothing.co.za
an online clothing store that produces clothing pieces with a fashion of young teenagers and young adults with a dark aesthetic
port { motion } from "framer-motion";

export default function About() {
  return (
    <div className="max-w-3xl mx-auto space-y-8">
      <motion.div
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        className="prose prose-invert mx-auto"
      >
        <h1>About m1dnyt</h1>
        <p>
          m1dnyt is a contemporary fashion brand that embodies the spirit of
          urban culture and modern aesthetics. Founded with the vision to create
          clothing that resonates with the bold and the ambitious, we craft
          pieces that seamlessly blend style with comfort.
        </p>

        <h2>Our Story</h2>
        <p>
          Born from the streets and inspired by the night, m1dnyt represents
          the creative energy that comes alive after dark. We believe in the
          power of self-expression through fashion and create pieces that
          empower individuals to tell their unique stories.
        </p>

        <h2>Our Vision</h2>
        <p>
          We strive to push the boundaries of contemporary fashion while
          maintaining our commitment to quality and sustainability. Each piece
          is thoughtfully designed and crafted to stand the test of time, both
          in style and durability.
        </p>
      </motion.div>
    </div>
  );
}
import { motion } from "framer-motion";

export default function About() {
  return (
    <div className="max-w-3xl mx-auto space-y-8">
      <motion.div
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        className="prose prose-invert mx-auto"
      >
        <h1>About m1dnyt</h1>
        <p>
          m1dnyt is a contemporary fashion brand that embodies the spirit of
          urban culture and modern aesthetics. Founded with the vision to create
          clothing that resonates with the bold and the ambitious, we craft
          pieces that seamlessly blend style with comfort.
        </p>

        <h2>Our Story</h2>
        <p>
          Born from the streets and inspired by the night, m1dnyt represents
          the creative energy that comes alive after dark. We believe in the
          power of self-expression through fashion and create pieces that
          empower individuals to tell their unique stories.
        </p>

        <h2>Our Vision</h2>
        <p>
          We strive to push the boundaries of contemporary fashion while
          maintaining our commitment to quality and sustainability. Each piece
          is thoughtfully designed and crafted to stand the test of time, both
          in style and durability.
        </p>
      </motion.div>
    </div>
  );
}
import { motion } from "framer-motion";

export default function About() {
  return (
    <div className="max-w-3xl mx-auto space-y-8">
      <motion.div
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        className="prose prose-invert mx-auto"
      >
        <h1>About m1dnyt</h1>
        <p>
          m1dnyt is a contemporary fashion brand that embodies the spirit of
          urban culture and modern aesthetics. Founded with the vision to create
          clothing that resonates with the bold and the ambitious, we craft
          pieces that seamlessly blend style with comfort.
        </p>

        <h2>Our Story</h2>
        <p>
          Born from the streets and inspired by the night, m1dnyt represents
          the creative energy that comes alive after dark. We believe in the
          power of self-expression through fashion and create pieces that
          empower individuals to tell their unique stories.
        </p>

        <h2>Our Vision</h2>
        <p>
          We strive to push the boundaries of contemporary fashion while
          maintaining our commitment to quality and sustainability. Each piece
          is thoughtfully designed and crafted to stand the test of time, both
          in style and durability.
        </p>
      </motion.div>
    </div>
  );
}
import { Link } from "wouter";
import { Search, ShoppingBag, Menu } from "lucide-react";
import { Button } from "@/components/ui/button";
import {
  Sheet,
  SheetContent,
  SheetTrigger,
} from "@/components/ui/sheet";

export default function Navbar() {
  return (
    <nav className="border-b bg-background/95 backdrop-blur supports-[backdrop-filter]:bg-background/60">
      <div className="container flex h-16 items-center px-4">
        <Sheet>
          <SheetTrigger asChild>
            <Button variant="ghost" className="md:hidden">
              <Menu className="h-5 w-5" />
            </Button>
          </SheetTrigger>
          <SheetContent side="left">
            <div className="flex flex-col gap-4 mt-8">
              <Link href="/">Home</Link>
              <Link href="/products">Shop</Link>
              <Link href="/about">About</Link>
              <Link href="/contact">Contact</Link>
            </div>
          </SheetContent>
        </Sheet>

        <div className="flex w-full justify-between items-center">
          <Link href="/" className="text-xl font-bold">
            m1dnyt
          </Link>

          <div className="hidden md:flex items-center gap-6">
            <Link href="/">Home</Link>
            <Link href="/products">Shop</Link>
            <Link href="/about">About</Link>
            <Link href="/contact">Contact</Link>
          </div>

          <div className="flex items-center gap-4">
            <Button variant="ghost" size="icon">
              <Search className="h-5 w-5" />
            </Button>
            <Button variant="ghost" size="icon">
              <ShoppingBag className="h-5 w-5" />
            </Button>
          </div>
        </div>
      </div>
    </nav>
  );
}
import * as React from "react"

import type {
  ToastActionElement,
  ToastProps,
} from "@/components/ui/toast"

const TOAST_LIMIT = 1
const TOAST_REMOVE_DELAY = 1000000

type ToasterToast = ToastProps & {
  id: string
  title?: React.ReactNode
  description?: React.ReactNode
  action?: ToastActionElement
}

const actionTypes = {
  ADD_TOAST: "ADD_TOAST",
  UPDATE_TOAST: "UPDATE_TOAST",
  DISMISS_TOAST: "DISMISS_TOAST",
  REMOVE_TOAST: "REMOVE_TOAST",
} as const

let count = 0

function genId() {
  count = (count + 1) % Number.MAX_SAFE_INTEGER
  return count.toString()
}

type ActionType = typeof actionTypes

type Action =
  | {
      type: ActionType["ADD_TOAST"]
      toast: ToasterToast
    }
  | {
      type: ActionType["UPDATE_TOAST"]
      toast: Partial<ToasterToast>
    }
  | {
      type: ActionType["DISMISS_TOAST"]
      toastId?: ToasterToast["id"]
    }
  | {
      type: ActionType["REMOVE_TOAST"]
      toastId?: ToasterToast["id"]
    }

interface State {
  toasts: ToasterToast[]
}

const toastTimeouts = new Map<string, ReturnType<typeof setTimeout>>()

const addToRemoveQueue = (toastId: string) => {
  if (toastTimeouts.has(toastId)) {
    return
  }

  const timeout = setTimeout(() => {
    toastTimeouts.delete(toastId)
    dispatch({
      type: "REMOVE_TOAST",
      toastId: toastId,
    })
  }, TOAST_REMOVE_DELAY)

  toastTimeouts.set(toastId, timeout)
}

export const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case "ADD_TOAST":
      return {
        ...state,
        toasts: [action.toast, ...state.toasts].slice(0, TOAST_LIMIT),
      }

    case "UPDATE_TOAST":
      return {
        ...state,
        toasts: state.toasts.map((t) =>
          t.id === action.toast.id ? { ...t, ...action.toast } : t
        ),
      }

    case "DISMISS_TOAST": {
      const { toastId } = action

      // ! Side effects ! - This could be extracted into a dismissToast() action,
      // but I'll keep it here for simplicity
      if (toastId) {
        addToRemoveQueue(toastId)
      } else {
        state.toasts.forEach((toast) => {
          addToRemoveQueue(toast.id)
        })
      }

      return {
        ...state,
        toasts: state.toasts.map((t) =>
          t.id === toastId || toastId === undefined
            ? {
                ...t,
                open: false,
              }
            : t
        ),
      }
    }
    case "REMOVE_TOAST":
      if (action.toastId === undefined) {
        return {
          ...state,
          toasts: [],
        }
      }
      return {
        ...state,
        toasts: state.toasts.filter((t) => t.id !== action.toastId),
      }
  }
}

const listeners: Array<(state: State) => void> = []

let memoryState: State = { toasts: [] }

function dispatch(action: Action) {
  memoryState = reducer(memoryState, action)
  listeners.forEach((listener) => {
    listener(memoryState)
  })
}

type Toast = Omit<ToasterToast, "id">

function toast({ ...props }: Toast) {
  const id = genId()

  const update = (props: ToasterToast) =>
    dispatch({
      type: "UPDATE_TOAST",
      toast: { ...props, id },
    })
  const dismiss = () => dispatch({ type: "DISMISS_TOAST", toastId: id })

  dispatch({
    type: "ADD_TOAST",
    toast: {
      ...props,
      id,
      open: true,
      onOpenChange: (open) => {
        if (!open) dismiss()
      },
    },
  })

  return {
    id: id,
    dismiss,
    update,
  }
}

function useToast() {
  const [state, setState] = React.useState<State>(memoryState)

  React.useEffect(() => {
    listeners.push(setState)
    return () => {
      const index = listeners.indexOf(setState)
      if (index > -1) {
        listeners.splice(index, 1)
      }
    }
  }, [state])

  return {
    ...state,
    toast,
    dismiss: (toastId?: string) => dispatch({ type: "DISMISS_TOAST", toastId }),
  }
}

export { useToast, toast }
